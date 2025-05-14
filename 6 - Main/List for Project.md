- User creates an a workspace for their given organisation, giving it a name , providing their own credentials, deciding if it's done on cloud or on their local server and then create a admin username and password they can use to log in with

Data Source
- They add the credential details of the data sources they want to add, including all the details necessary for it as well as name, description, type, frequency of updates (if eligible for example static files)
- For streaming data they have the option to batch store it in a permeant storage location on the production database to be queried as a batch process, and conditions for that should be specified as well as how that would like in terms of information stored
- They have to specify if the data source is speed layer eligible (e.g. If they can use CDC in order to read database, if data is append only, frequency of reading the data, frequency of the data source being uploaded)
- Should be able to test connection to see if it can actually connect to it securely, as well as giving time taken to ping it
- Should be able to view how often that data source is used, (how many queries it's involved in , rate of transfer of data from that source, what batch processes it's involved in, dependencies essentially)
- If it's static file or something being streamed or something for example, could have a preview of the data being read from it
- Want to be able to view all data sources and their information regarding them in the sidebar, such as name, type, when it was created
- Want to be able to add a view to view credential of information with password greyed out of Couse
- Should only be able to delete those without dependencies and should come with a warning.
- Should link to the relevant pipeline batches for those in the list

Query
- They will want to write queries against these data sources
- Should be able to view all the data sources that are available to query on the side including the tables, previous queries and batch views etc.
- For the output should be able view the data/ columns available
- For the input, should be able to view the input components and the type required
- If query isn't just streams should have an option allowing speed layer in order to show the metadata also stored a long the request
- Should be able to test the query
- Should say if it's just using speed layer, batch layer or both based on the query (although it will always back up to query)
- 


Pipeline
- Want to be able to create an ETL pipeline to start the batch layer process, making sure to version all data, add time stamps and create star schema tables if necessary
- For 
- Should be able to create star schema tables as necessary for any features they like
- Should be able to view all the dependency's for a given star schema
- Should be able to have a standard full refresh time of 2 am per week but can specify for any individual process what time they want to fully refresh
- Show the query for Extraction as well as the different steps added during the transformation stage, such
- should have multiple different extraction for each specific source of data needed with filtering and basic Computation if possible 
- so we have a built up connection for tables in the staging area
- have some base transformation steps like indexing versioning, typing columns timestamping
- determine how they load by either loading as raw data as is or as part of other data via a regular query or specifically a star schema fact table. Regardless the querying will only allow those tables that have been transformed


Dashboard
- Dashboards are just a culmination of adding queries and formatting with the edit page into a dashboard.
- Each component should have button on it's top left in to open a toggle bar in order to give more configuration information about the data sources
- Configuration should tell them: what data sources are included, including their names, type, last refresh rate and description, queries involved, amount of data returned from the actual query, amount of data to render component on page, time taken for query. Also Should be able to view the raw output for the option
- That button on the top left corner should have a different coloured icon depending on how out of time it is, so blue 0-2 , orange 2-10 red 10 - more.


Edit Dashboard
- Note: For containers, just make it simpler and add a border so if they overlap, it's not a big concern
- When building the page, User may want to section page into different sections, so need to divide the page into 16 columns with N rows
- Need to have a section 1. For Sectioning having a container with a title /non optional title. 2. Outputs for map, cards, graphs, tables and text 3. Inputs for text, drop down
- Need to be able to save
- Need to be able to preview the page and open in a new tab
- each component should have a ID, possible title as well as position 
- Need to have a section for basic component information like type, colour, position and another for data which should allow different slots for different columns depending on the data 