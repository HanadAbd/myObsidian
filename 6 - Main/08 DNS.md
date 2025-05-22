2025-01-14 10:40

Status:

Tags:[[Advanced Networking]]

---
**NOTE:**
- **NS is Name Server**
A Domain Name System (DNS) is a system used to map human-readable domain names to IP addresses, enabling the location of resources on the internet.

DNS operates hierarchically, starting from the root (`.`), progressing to top-level domains (TLDs) like `.com` or `.uk`, then second-level domains (e.g., `ac`), and finally subdomains or specific hosts (e.g., `example.ac.uk`).

Each node in the hierarchy corresponds to a resource record (RR), which stores key-value pairs:
- **Key**: Fully Qualified Domain Name (FQDN).
- **Values**: Time to Live (TTL), class (`IN` for Internet), type (`A`, `AAAA`, `MX`, etc.), and associated data (e.g., an IP address).

==Types can be:==
- ==A (Ipv4)==
- ==AAAA (IpV6)==
- ==MX (mail exchangers)==
- ==NS (Name Servers)==

==RR sets is when there are multiple records for a given name==


![[Pasted image 20250114172838.webp|608]]
A **zone** is a portion of the DNS namespace, served by one or more name servers. The zone file contains resource records for that zone. Zones are managed by primary (holds the original zone file) and secondary servers (synchronize via zone transfers), both of which are authoritative.


DNS resolution involves:
1. A client querying a ==recursive server==.
2. The resolver contacting root, TLD, and authoritative servers to find the answer.
3. Recursive communication down the hierarchy until the domain is resolved.

Authoritative servers provide definitive answers for their zones, while recursive resolvers facilitate queries and caching.

### DNS message
---

![[Pasted image 20250114172936.webp|780|709x212]]

This is an example DNS packet sent between client and DNS (of course not initially complete when sent by client but is completed by DNS):
- **Transaction ID**: Unique Identifier for the query/response pair set by client
- **Flags**: Indicate query/response type, recursion, and status codes.
- **Question Count**: Counts for questions and resource records in answer, authority and additional section
- **Question**: The query, or the query being answered (on the way back)
- **Answer Records**: response to queries
- **Authority records**: Where these records are from
- **Additional records**: any stuff the server also gives to client which they might find useful (addresses for Name Servers or Mail Servers, in particular) which can be helpful for caching

==DNS clients are known as resolvers and are used to make direct queries to the DNS==

### Different Flags and Bits
---
- Bit 0: 0 is question, 1 response
- Bits 1-4: Opcode to define kind of query (e.g. DNS lookup, or server status request)
- Bits 5-8: Different individual flags: 

| Bit | Flag                          | Meaning                                                         |
| --- | ----------------------------- | --------------------------------------------------------------- |
| 5   | **AA (Authoritative Answer)** | Is the answer from an authoritative server? (Only in responses) |
| 6   | **TC (Truncated)**            | Message too big for UDP; try again using TCP.                   |
| 7   | **RD (Recursion Desired)**    | Client is asking for recursion (almost always set).             |
| 8   | **RA (Recursion Available)**  | Server confirms recursion is supported (in response).           |
- Bits 9-11: reserved
- Bits 12-15: RCODE (Response Code) which defines status/quality of the response e.g. (No error, or domain name doesn't exist etc.)


### Full DNS Process

1. **Query Initiation by the Client**:
    - The client application (e.g., a browser) needs to resolve a hostname (e.g., `www.example.com`) into an IP address.
    -  It invokes the  **resolver** in the OS or application, which first checks **local caches** (application cache, OS DNS cache, hosts file). If no record is found, it creates the query setting the “recursion desired” flag to a **recursive server**.
2. **Recursive Server Role**:
    - The recursive server ==(often run by your ISP, corporate network, or a public DNS service like 1.1.1.1 or 8.8.8.8)== handles the query and checks its own cache. If failed, the resolver starts querying external DNS servers from root server
    - The recursive resolver queries one of the **root DNS servers** (pre-configured in the resolver). These servers are responsible for directing queries to the appropriate **Top Level Domain server** responsible for e.g.(.com, .uk, .tld etc.).
    - ==The root returns with the closest NS it knows e.g. `.com` or `example.com`==
3. **TLD Server Query**:
    - The resolver queries the TLD server for the domain name (e.g., `example.com`).
    - The TLD server responds with the location (NS record) of the **authoritative name server** for the domain.
4. **Authoritative Name Server Query**:
    - The resolver queries the authoritative name server for the specific hostname (e.g., `www.example.com`).
    - If authoritative responsible for the requested domain, it provides the required **Resource Record (RR)** (e.g., `A`, `AAAA`, or `MX` records containing the IP address or mail server).
    - Otherwise if delegated, returns NS records pointing to the net name server closer query
5. **Cache and Respond**:
    - The recursive resolver caches the result for future use, respecting the **TTL** value from the resource record.
    - It then sends the resolved IP address back to the client.

### Label and compression
---
**Domain names** in the resource record are broken down into labels, with a maximum length of 63 bytes for each label. *Label Compression* works as follows:

1. Each label is prefixed with a byte for its length (e.g., `[3] foo [3] dom [3] ain [0]` for `foo.dom.ain` starting at byte 48).
2. For `mail.foo.dom.ain`, we can compress by pointing to the domain starting at byte 48: `[4] mail [192] [48]`.

The byte `192` (0xC0) is a pointer, with the next 6 bits combined with the byte to specify the 14-bit offset. So allows use to reuse domains labels from earlier in the **domain name**.

### Caching
---

At each stage, everyone caches the data they get, especially the recursive servers with information of NS records for popular domains (refreshed once per TTL seconds).

- ==Clients cache resolved addresses (often managed by the OS)==
- ==Recursive servers build extensive caches of popular domains==
- ==All cached records respect their TTL values, which decrease over time==
- ==When TTL expires, a fresh lookup must be performed==

==Modern recursive servers implement "bailiwick checking" - only accepting and caching information that servers are authoritative for, preventing cache poisoning attacks.==

### ==SOA (Start of Authority) Records==

==---==

==SOA records define authoritative information about a DNS zone:==

```
cs.bham.ac.uk. 86400 IN SOA dns0.cs.bham.ac.uk. hostmaster.cs.bham.ac.uk. (
    2015022000 ; serial
    10800      ; refresh (3 hours)
    3600       ; retry (1 hour)
    604800     ; expire (1 week)
    86400      ; minimum (1 day)
)
```

- ==**Serial Number**: Version identifier, incremented when zone changes==
- ==**Refresh**: How often secondaries check for updates==
- ==**Retry**: How long to wait before retrying if refresh fails==
- ==**Expire**: Maximum time secondaries serve data without successful refresh==
- ==**Minimum**: Originally for all records; now primarily for negative caching==

### ==Zone Transfers and Delegation==

==---==

==**Zone Transfers**: Process where secondary servers obtain zone data from the primary:==

- ==AXFR: Full zone transfer (entire zone)==
- ==IXFR: Incremental zone transfer (only changes)==
- ==Should be restricted to authorized secondaries==

==**Delegation**: Process of assigning authority for a subdomain:==


```
cs.bham.ac.uk. 28800 IN NS dns0.cs.bham.ac.uk.
cs.bham.ac.uk. 28800 IN NS dns1.cs.bham.ac.uk.
cs.bham.ac.uk. 28800 IN NS ns0.susx.ac.uk.
```

==**Glue Records**: A records in parent zone that provide IP addresses for nameservers within the delegated domain itself:==


```
dns0.cs.bham.ac.uk. 28800 IN A 147.188.192.4
dns1.cs.bham.ac.uk. 28800 IN A 147.188.192.8
```
### ==Security Issues==

- ==**Old Attacks**: Old nameservers blindly accepted and cached additional information, allowing attackers to inject false records. Fix: "Bailiwick checking" - only accept additional information from authoritative sources==

- ==**Reverse Attacks**: Attackers controlling reverse DNS can create deceptive PTR records. **Defence**: Always verify forward/reverse record matches==

- ==**Kaminsky Attack** (2008): Uses DNS transaction ID prediction to poison caches:==
	1. ==Attacker floods recursive server with fake responses==
	2. ==If transaction ID matches an in-progress query, fake data is cached==
	3. ==Allows hijacking of entire domains Mitigations:==
	- ==Source port randomization (expanding entropy space)==
	- ==DNSSEC (Domain Name System Security Extensions) implementation that digitally signs DNS records==
	- ==Avoid DNS resolvers behind NAT==

- ==**DNS over HTTPS/TLS**: Encrypts DNS traffic, preventing monitoring/manipulation **Challenges**: Bypasses traditional network filtering, complicates security controls==


### ==Best Practices==

==---==

- ==Separate authoritative and recursive server functions - NEVER combine them==
- ==Implement proper access controls on all DNS servers==
- ==Use DNSSEC for critical zones where possible==
- ==Configure appropriate TTL values==
- ==Regularly audit and verify DNS configurations==
- ==Deploy redundant nameservers across different networks==


##### Glossary 
---
- ==**DNS**: Domain Name System; translates domain names to IP addresses and provides other resource information==
- **Domain**: Logical grouping of related network resources identified by a unique name within the DNS hierarchy. Broken down into Top Level Domains (TLD's), subdomains and fully qualified domain names (FQDNs)
- **Zone**: Stored and managed on authoritative servers as zone files, it's portion of the DNS namespace that contains resource records for the domain and possibly domains
- **Authoritative Server**: A DNS server that has the definitive, up-to-date information about a specific DNS zone. It provides answers to queries about domains in its zone and is responsible for maintaining the zone's records.
- ==**Recursive Server**: NS server that performs queries on behalf of a client to resolve a domain name, recursively querying other NS servers, caching result and returning answer.==
- ==**Resolver**: Client software that initiates DNS lookups==
- **Name Server**: Server that stores DNS records and respond to queries
- **Resource Record**: Data entry in a DNS zone file that provides information about domain or host. Such as IP address, A or AAAA record, class, TTL, data
- **TTL**: Time DNS record is considered valid, and be cached. Otherwise needs to be looked up eventually.
- **Domain Name**: Human readable address that are structured as labels separated "." 
- **Primary Server**: Authoritative DNS server holding original writable copy of zone file to be shared with secondary. 
- **Secondary Server**: Authoritative DNS server holding read-only copy of zone file. For load balancing and redundancy.

##### References
----
[08 DNS](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_10/08%20DNS.pdf)


![[08 DNS.pdf]]