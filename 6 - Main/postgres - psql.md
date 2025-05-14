2025-01-02 19:35

Status:

Tags:

---

**Naming Convention:**
- Plural Nouns for table names 
- Primary key is typically {table.name}_id
- Snake case so "order_date"

CRUD:
--
```
CREATE TABLE my_table(
	my_id INTGER PRIMARY KEY GENERATED ALWAYS AS INTEGER
	my_column TEXT,
	my_val INTEGER
);

INSERT INTO my_table (my_column,my_val) VALUES ("example",2) 

SELECT myCOLUMN from my_table 
WHERE my_ID = 1;

DELETE TABLE my_table;

```



Change database

```
//view all databases
\c <database name>

\c [ -reuse-previous=_`on|off`_ ] [ _`dbname`_ [ _`username`_ ] [ _`host`_ ] [ _`port`_ ] | _`conninfo`_ ]`

```

Change schema

``` shell
#View all schemas
\dn
```


Change user

¬¬

View all tables

```
// List all tables in the current schema
\dt
// List all tables across all schemas 
\dt *.*
```

view all databases

```
\l or \list
```

Working with dates:
--

Use


##### References


----
