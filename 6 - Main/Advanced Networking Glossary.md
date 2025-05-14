```dataview 
TABLE WITHOUT ID
file.link AS "Title",
definition AS "Definition",
topic AS "Topic",
related AS "Related"
FROM #vocabulary 
WHERE glossary = this.file.link
SORT file.name

```


- Protocol Stack

- HTTP
  Hyper Text Transfer Protocol, 
- HTTPS
- Switch
- Host
- Router
- Modem
- Port
  So you can use the ip address to connect to machine but in order to have multiple connections from a machine, you also have ports. Some important ports are reserved like http 80, https 443, ssh 20, dhs 53.
  If you want to connect to a machine, you'll need it's ip address as well as the port reserved for the connection.
- Requests
- Interface
  The point where a device connects to a network. Either physically or logically