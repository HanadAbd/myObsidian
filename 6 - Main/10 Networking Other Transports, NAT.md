2025-05-04 20:26

Status:

Tags: [[Advanced Networking]]

---
## Summary of NAT
---

Extends limited amount of public limited amount of public IPv4 addresses by translating many private addresses to fewer public ones, by physically changing packet header when it goes through NAT gateway in network router.

Provides brief security as rudimentary firewall but unreliable as full security solution. 

It violates End-to-end principle which states application specific features should be handled by end nodes. Meaning any host X should be able to connect to any host Y. NAT breaks this, but hiding Y and instead forcing use of public address Z. To be used. When Y communicates with X, Y's IP address is translated to Z, hence breaking end to end principle by prevents direct, bidirectional communication between arbitrary hosts on the internet.


### Network Interfaces
	
Any endpoint, either software or hardware, where systems receives/sends packets. This can include Ethernet Ports, Network ports and other physical and virtual interfaces. Each interface belongs to a host, managed by some system.



### Real-time Transport Protocol RTP

Majority of Transport protocols used are UDP and TCP. Other serious alternatives is a suite of transport protocols that focuses more on jittering and timing of packets e.g. in case of streaming or calls etc. 

Latency is a big issue for video calls, especially when it comes to echoes


![[image-3.png]]

RTP is typically only used for voice calls


- Used for voice (telephony) and video streaming applications
- Provides functionality similar to what can be implemented with UDP
- Addresses timing consistency issues critical for real-time applications

Features:
- RTP provides a timestamp and sequence number, in order to identify bit rate of the stream.
- No acknowledgments (unlike TCP) but receiver discards packets to discard or pauses and waits based onit telling if a packet is missing.
- ==Duplicates are detected==
- ==Video streams are setup with RTCP (Real Time Control Protocol) and Voice for IP Telephony with SIP (Session Initiation Protocol)==

==Typically, streaming handles this with **TCP and buffering**, so jittering of packets so instead of immediately displaying what ever comes in, it assumes there is lower bandwidth e.g. getting next 30 seconds. Although you can't do this==



### Multipath TCP

Allows multiple paths to be used by one TCP connection, for example Wi-Fi and 4G simultaneously, in order move  seamlessly over one the other instead tearing down TCP connection and starting a new one. Endpoints on either side would select which path is better, increasing performance and fault tolerance with redundancy.


### Address Exhaustion

==Limited amount of IPv4 addresses. Especially with Poor Distribution. Certain addresses are made private for isolated networks not connected to the internet network, now hidden between NAT gateways to preserve public addresses and allow multiple private addresses for 1 public IP address. Provides local addressing flexibility by allowing you to freely assign any private address, since only the public one is used.== 

==**RFC 1918 private ranges:**==
- ==10.0.0.0/8==
- ==172.16.0.0/12 (i.e. 172.16.0.0–172.31.255.255)==
- ==192.168.0.0/16 .==
### Proxying

Proxying is 1 solution for Address Exhaustion.
Proxies are protocol-aware applications that terminates client connections on one interface, and instead makes outbound connections on another.


**Characteristics:**
- Custom per-protocol (e.g. HTTP, FTP) → client must support the proxy
- Can provide caching, logging, content inspection, access control
- BUT more resource intensive, complex add additional latency.

### Network Address Translation (NAT)

Technique used to map various private IP addresses to fewer public exposed addresses, In order to hide the internal workings of the internal network. This is done by literally changing the header of packets during routing to be other IP address.

Breaks end to end principal but conservers addresses. Meaning there is interference between sender and receiver, due to NAT

Two Modes:

TCP connections are uniquely identified by a combination of source IP, source port, destination IP, and destination port.

1. **Outbound (source) NAT:**
	- Rewrites source IP:port → (public IP, unique source port) (unique port is used to identify the private network)
	- Maintains a translation table mapping (pub IP, pub port) ↔ (priv IP, priv port)
	- TCP connections are uniquely identified by a combination of source IP, source port, destination IP, and destination port.
	- Modern NAT implementations typically allow up 65535 concurrent connections for each distinct source port number each connection is on.
	
2. **Inbound (destination) NAT:**
	- Listens on public IP:port and forwards to multiple internal hosts/ports
	- Enables hosting many services behind one IP (load-balancing, failover)


### NAT working with TCP

**Stateful**: On seeing a TCP SYN, mappings are made between inside and outside addresses for new connection. Packet headers are modifed and checksums recluclated. When connection properly completes with FIN packets, mappings are removed.

### NAT working with UDP

UDP is connectionless, so UDP NAT operates without connection state, just rewriting IP header of outgoing packets. Return packets are accepted until a time out of 10 seconds typically.

A limit on amount of replies can also be imposed

### Problems with NAT

Difficult to authenticate, and log. Most web logging, does not record source ports, although it could

1. **Difficult to Authenticate and Log**, since multiple users appear as single IP and web server logs rarely include source ports.
2. **Protocol Breakage**: Specialised NAT modules are required due to NAT breaking protocols like FTP which send addressing information in control channel, so addressing information within their payload. This would require inspection and modification of packet content, which increases complexity and resource usage. e.g. Passive Mode fixes by having server tell the client which port to use instead of the other way.
3. **Port‐pair exclusivity:** Any given `(public-IP, public-port)` can only map to a single `(private-IP, private-port)`. Requires work arounds for protocols that use well known defined ports (e.g. DNS on UDP/53 or HTTP on 80). Without work-arounds (multiple public IPs, alternate ports, or application-level proxies), you’re limited to servicing one internal host per public port, which can block deployments of multiple identical‐port services.
4. **False Security Assumptions**: NAT is not designed for security but is treated as such, despite inbound NAT providing no security, with pass through connections to internal hosts.
5. **IoT Limitations**: Inhibiting direct device addressing inhibits IoT development, with solutions like Carrier Grade NAT by service provider, resulting in double NAT scenarios, further complicating end to end connections.
6. **UPNP (Universal Plug and Play) abuse**: Opens door to malware by allowing inside device to ask NAT point and request inbound NAT, bypassing of any firewall.

### IPv6 and NAT

- IPv6 designed without NAT requirement due to abundant addresses
- Many IPv6 implementations don't support NAT

### ==Reverse Proxies and Dedicated Proxy Server==

==Modern day alternative for NAT when it comes to replacing Inbound NAT and distributing messages from the internet to private addresses.==

==Reverse proxies act as a middle man for input messages, forwarding good requests to internal servers, and enforcing rate‐limiting, URL filtering, request inspection, etc.==

==Dedicated Proxy server goes further, but also caches responses, compress traffic, or provide Web Application Firewall (WAF) features.==

##### References
----
[08 Networking Other Transports, NAT](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_8/08%20Networking%20Other%20Transports,%20NAT.pdf)
![[08 Networking Other Transports, NAT.pdf]]
[Lecture](https://bham.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=c5ed26d6-90ce-4d04-ad3d-b2340094c036)

