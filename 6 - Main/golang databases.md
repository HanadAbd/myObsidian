2025-01-05 12:57

Status:

Tags: [[golang databases]]

---

Different drivers to use:

```
// Postgres github.com/lib/pq
// Mssldb github.com/denisenkom/go-mssqldb
// Oracle github.com/godror/godror
```

Universal standard library called "database/sql" that will be used the most. None of these change the interface from that database/sql but they do enable connections and  add to the it with changing the API like for example **translating go types to that language** 

So you only need to initialise a connection with the corresponding driver, and then it will work forever.



Querying a data source

```
/* You need to first create a connection string of the necesssary datasources and then pass a query to it.
*/
package main
import(
 _ "github.com/lib/pq"
)

var (
	username:= "postgres"
	password:= "Week7890"
	hostname:= "localhost"
	port:= "5432"
	database:= "postgres"
)

func main(){
	constr := fmt.Sprintf("user=%s password=%s dbname=%s host=%s port=%d sslmode=%s",
	username, password, dbname, hostname, port, sslmode)
	//the first arugment defines the database based on the driver used e.g postgres,mssql, godror
	db,_ := sql.Open("postgres", constr)

	query:= "SELECT * FROM public.users;"

	row , _ := db.Query(query,<any arguments if you need them>)
}

```

Getting returned query data

First of all use **db.Query** instead of **db.Exec** for queries where you expect a return value e.g. SELECT statements.

What's returned is of the type `*sql.Rows` which is a pointer to a series of rows. With the pointer being behind the data.

You can commands **.next()** to move the cursor to the next row and **.scan()** to map these values to a variable to use 


```
values := make([]interface{}, len(columns))
    for i := range values {
        values[i] = new(interface{})
    }
    for rows.Next() {
        rows.Scan(values...)
        for i, col := range values {
            fmt.Printf("%s (%s): %v\n", columns[i], columnTypes[i].DatabaseTypeName(), *(col.(*interface{})))
        }
    }
```


Getting Colum

```
rows,_:= db.Query(query,args)

//This just returns a []string of the column names
columns,_ := rows.Columns()

//Get's more information like column type,name,length, nullable etc. but how much is avilable is up to driver being used.

columnInfo,_ :=rows.ColumnTypes()
```


Verifying connection:
--

```
err:= db.Ping()
```

Verifying if there still is a connection of ever was in the first place. Useful for reconnecting if need be

Working with dates
---

You can just use regular golang **time.time** fields. So just past the time line necessary as a parameter.
```
query:= "SELECT * FROM time_example WHERE day <= $1"
row,_ := db.Query(query,time.Now())
```


##### References


----
