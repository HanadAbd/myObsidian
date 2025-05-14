2025-03-17 09:45

Status:

Tags: [[Programming]]
[[Final Year Project]]

---

***Key Database configurations that need to be considered***

- Users Data
- Configuration data for user/application
- Handling Application Data
- Storing Metadata for application
- 
  
- Session Redis table:
  This would contain metadata

***Models for database and server***

Main things to consider are:

- If you want to partition database with **schema** or some **tenant identifiers**
- If **configuration database** and **application database** are the same database or not. Doesn't even need to be the same type
- Importance of separating workspaces, since this will determine if multiple schemas, multi-tenant design or completely separate databases.
- If their is single database for multiple workspaces, or separate data per workspace
  
  
So for our project, we'll have 2 solutions. 1 on premise solution we'll spend most of our time doing. So that means 1 production database that handles both configuration and stores all application data a tenet column (workspace ID) column used to differentiate them, with queries to filter by them and index by

so both
`APP_ENV = dev/prod`
`APP_LOCATION = cloud/local`



Regardless we should have an admin view over the entire application to measure performance, how many workspaces, how it's separated across servers. This should also be where the server view should be



##### References
----
