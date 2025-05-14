2025-01-12 14:13

Status:

Tags: [[Advanced Networking]]

---

What is HTTP:
---

Hyper Text Transfer Protocol is a protocol used originally for webpages and serving HTML and other content. It uses 1 TCP connection in order to pass data back and forth. Talks over Port 80 for HTTP and Port 443 for HTTPS, a more secure version of HTTP.
HTTP requests can be sent in various modes such as GET, POST, PUT,DELETE and HEAD.
It can send parameters with the URL and how the server or client interprets them is entirely up to them, whether that be as file directory, database parameters etc.

FTP:
---

File Transfer Protocol that's used to transfer files over connections.


Uses 2 main connections,
- **Control Connection** from client to server, used to send commands/Reponses. Sends IP/Port information for server to connect to. Easy to mark end of messages.
- **Data Connection** which actually bases the unknown sized file (so Can't embed EOF markers in Data). Created Per transfer and closed after completion.

##### ==How it works (in Active Mode)==

1. ==Client opens a **Control Connection**.==
2. ==For each transfer, Client opens random Listening socket, and IP/Port pair of socket is sent over control connection==
3. ==Socket is blocked, waiting for call back from server.==
4. ==Server uses information to make connection to listening socket.==
5. ==Repeats from step 2 for each data transfer==  


In **active mode**, data connection built by server goes to a random port of client (requires help to overcome firewalls and NAT), where as **passive mode** is client to random server port.

Passive mode solves the NAT problem but still issue with Fire Wall.

### Problems with FTP
- Uses a lot of connections
- Legacy of simplex (one way and without full duplex channels) NCP (Pre-cursor to TCP) Connections.




What HTTP Requests Look Like:
---

1. Client sends commands, option and a blank line
2. Server sends information, blank line and some data

![[image-4.png]]
The request sent from client has the first line of http method, and the URL **after** the hostname and then the HTTP version. This is because HTTP used to just be mapped from IP to IP so ignored host name but that is increasingly more important.
**Host** includes the namespace
**User-Agent** says who is making the request, e.g. what browser, device, application etc. Usually because it would have to be rendered differently for that device. 
**Accept** indicates what kind of _response from the server_ a client can accept


Types of request include GET, POST ,and less used DELETE and HEAD.
### ==HTTP Response==

You can have various other options with HTTP initialisation in order to aid performance/connection and the security.


- **HTTP Status code** : 1xx being information response, 2xxx successful, 3xx redirection etc. Only optional response
- **Content Type**: Explains how to render it
- **Content length**: Might missing if unknown while sending
- **Keep Alive** : Essentially just saying to keep this connection alive and not start a new one since it will be used again. 
- **Last Modified/E Tag** : So using the last modified date or even better, the hash of the request and checking with the server if that endpoint has changed results. If not, no point in returning and better off getting data from client side cache. More efficient
- **Strict-Transport-Security**: If a user connects via http, It is redirected to the https equivalent, with **max-age**  time for how long it will do that redirection.

### Issue with Transferring Files

1 common issue with transferring files was trying to find the end of the actual file size. If you know what is before hand, then you can add some information on the header of whatever protocol you're using to state that, but if not, like transferring over a compressed backup, something you can't know before hand, it's impossible. Requiring the other side to read through byte by byte the data, until it reaches the end of the data received.

So to avoid doing this as much as possible, each HTTP response **tries** to have length field

### Passing Arguments

Can pass parameters within the URL, typically through the convention of  `/query?var1=value1` Allowing GET's and it's arguments viewable as logs

### Defining Client what Clients Accept

**Accept-encoding** can define what encodings it can handle e/g/ deflate, gzip where server in  it's reply via **content-encoding** can define it e.g. gzip

Same for **Accept-Language**, and **Accept-Charset**

### HTTP Authentication

HTTP Basic AUth is done via sending Authorization tag with and encoding of `username:password` e.g. Base64encoding, otherwise return 401 unauthorised code

### Cookies

All requests are sent with a cookie header from a given domain/host which is updated with "Set Cookie " operation as key/value pair with a lifetime. Commonly used with HTTPS to protect username and password, and return cookie as token for successful authentication, and then ==rely on that being safe to pass unencrypted data, but ideally, HTTPS can be used for all operations.== 

==Generally, cookies store client side state: navigation, shopping carts etc.==

==Ideally as much should be done as server side as possible, with cookies limited to random session ID's==

### Caching

Ideally, cache static and repeatedly used content, whilst not interfering with dynamic/rare/slow content. Could be used on the edge of both a **producing** network, or **consuming** network




##### References

----
[07 HTTP and Friends](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_9/07%20HTTP%20and%20Friends.pdf)

![[07 HTTP and Friends.pdf]]

[Lecture 29 Nov](https://bham.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=d15415a8-c837-40b9-80d7-b2370094493d)

