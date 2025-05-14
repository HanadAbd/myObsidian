Using Server sent events, to continuously get live data from the "database". 

With Kafka streams, it's even easier since we can just read the Kafka stream and upload it to the front end.


We can set up a trigger on the database so with every insert statement to that database, will trigger the web socket and pass predefined query results to the server. This can then be passed to the front end to do whatever we may want.

There's the issue of storing content on the database or on the server. It's more stable and persistent to store on the database, but the constant queries to get variables would add up quite a bit of time and database usage.

Doing it on server get's rid of these disadvantages but at the cost of persistence and stability.  It would also mean queries would be taken directly from the database via a RestAPI call but real time data would be taken from the server. We would also have to consider buffers, managing that size dynamically and not deviating the final code too far from a regular query. Since we're going to add caching later anyway, this was an issue we were going to have eventually.

Could do a hybrid approach of both. Use the variable on the server for the most part, and every now and then, update the variable on the database.

On server initialisation, get the data from the server. So in case of server crash we can pick up where we left off. Technically we could just make the variable be a query that we can calculate from the database, but that assumes the data on the database will last forever or isn't a combination from other more complicated things that would be hard to put together. 

It's worth considering.

Also, not too hard for postgres or kafka streams, but we would kind of need a universal approach for most databases, excels and JSON files. Loading these all on to the server might not be ideal


#### Better Changes

- Could