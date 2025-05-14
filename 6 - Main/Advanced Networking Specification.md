H: High Understanding
M: Medium Understanding
L: Low Understanding

**Networking introduction:**

Packet switching and advantages over circuit switching 
Data flow metrics: volume (bandwidth), latency, error rate. Know how to calculate the time it takes to transmit some data across a link
Virtual circuits vs datagram services
DoD 4-layer model. Know the advantages of DoD model over the OSI model
Network elements: hosts, switches and routers

**Lower layers:**

Know what LANs and WANs are
Ethernet: how it works, especially dealing with collisions, ethernet devices
Advantages of ethernet over ATM
Switching issues and fixes, traffic shaping and policing

**IP:**

IP responsibilities, design and (lack of) guarantees
Reasons for deprecation of fragmentation
IPv4 addresses, basic routing, allocation, subnetting
Private IPv4 addresses
IPv6, advantages over IPv4
IP on lower layers, ARP

**Address allocation:**

Static allocation and reasons for use
DHCP operation, design and problems
IPv6: DHCPv6, SLAAC, RFC4941 (random addresses), RFC7217 (stable and opaque)

**Multiple interfaces:**

Link Aggregation
VLANs
Load balancing
VRRP
Any casting

**Transport layers:**

TCP vs UDP guarantees and comparison
TCP vs UDP demultiplexing
TCP operation in detail
TCP extensions such as selective acknowledgements and window scaling

**NAT and unusual transports (added 11/04/25):**

RTP
Multipath TCP
RFC1918 Proxying
NAT operation
NAT differences for TCP and UDP
NAT problems

**HTTP:**

Problems of FTP
Operation of HTTP

**DNS:**

DNS architecture and operation
DNS problems




### Professor's Spec

- *Transmission: ATM, WDM, SDH (all at a very high level only)* 
- Ethernet: switching, collisions, bridging, broadcasting, VLANs, Link Aggregation
- IP: addressing, IPv4 and v6 subnets and prefixes, *routing, routing protocols (OSPF, RIP, convergence properties)*, NAT
- UDP: applications, advantages and disadvantages
- TCP: applications, advantages and disadvantages, mechanisms and operation, sequence numbers, receive windows, slow start, window scaling, PAWS, timestamping, multi-pathing
- DNS: concepts, resource records, RR sets, basic operation, recursive and authoritative servers, caching
- Higher layer protocols: Basic operation of HTTP, FTP, *SMTP*

*Cut or extremely unlikely content *