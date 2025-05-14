2025-01-08 12:18

Status:

Tags: [[Advanced Networking]]

---

What happens when you go to https://www.bbc.co.uk/ or any site?

We're trying to connect to that host address and it's port. In general the process is:
1. parse the URL
2. convert the DNS to an ip address
3. create a TCP connection to that address
4. finally sending data across via a secured http request.

**Parsing the URL:**

Typically done with getting the host name and path, e.g. **`scheme://host/path`** where scheme decides how the rest of the URL is interpreted e.g. https or mailto, host being the www.bbc.co.uk and whatever coming next being the path on that host.

So DNS is used to convert the domain name given, into a viable ip address and ports.

IP (v4) addresses is a 32 bit address unique id for a given machine, divided into 4 bytes and a . e.g. 255.255.255.255   

Since ip v4 is 2^32 is only 4 billion, we are more commonly using ipV6 which we've moving towards collectively since the mid 2000s and is 64bit, which is more then enough.

When it comes to ports, these are just the multiple possible connection points you can have to a given machine, e.g. ssh being 22, DNS being 53, http is 80. These are just reserved ports for default machine services. So when we do port 8080 or something, we're reserving a new port for just our new app.

So in our case, we're connecting to port 443 (for https) on the www.bbc.co.uk which when resolved by the DNS, converts it to an IP address to connect to. We then connect to it via a TCP Connection. Then we set up the security of the https connection by doing the TLS handshake approach and we can send http requests as much as you want.

TCP is just a network protocol used to connect a source host to a destination host and to send packets of data across. It's a very secure one since it, unlike UDP transfer protocol, doesn't just "send" data back and forth. It use's additional values to confirm if data sent is "Acknowleged" and "Sychronise" to account if the packet is meant to have complete data along side with it. More expensive but leads to a much more secure and stable connection.


##### References

[[RFC791 IP]]
[[UDP RFC 768]]
[[TCP RFC 9293]]

----
