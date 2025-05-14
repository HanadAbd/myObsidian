2025-01-15 10:19

Status:

Tags: [[Advanced Networking]]

---

### Link Aggregation (Link Agg)

Multiple cables and possible switches acting as 1 network. It combines all interfaces into 1 logical interface for a machine.  

==Especially useful modern solution in environments with high bandwidth requirements and where fault tolerance and throughput are critical==
##### ==Advantages of Link Agg==
- ==Only 1 IP address, and 1 entry in routing table.==
- ==Failure detection much faster and simpler as done at link level==
- ==Fast Failover==
- ==Efficient multiplexing and load spreading==
- 
==Con:==
- ==Only as far as nearest switch==
- ==Doesn't provide spreading over multiple internet connections==


### VLANS (Virtual Lan's)

**VLANS** logical networks for 1 physical networks, so multiple networks delivered over single cable. Useful for separating traffic whilst sharing the same physical infrastructure.

==Ethernet frame has optional 4 byte tag field to identify network supporting 1-4094 VLANS==

==Treated as separate networks by the OS and networking hardware.==

=="Router on a stick" refers to router using 1 physical connection, but creating multiple virtual connections to handle each VLAN, allwoing inter-VLAN routing with minimal Hardware==

==Ports can either be tagged or untagged:==

- ==**Untagged ports (aka "Access Ports")** are designed for end devices that don't understand VLAN tagging. Add's tag when frame enters, and removes when leaving. Each port is assigned a PVID for untagged traffic.==
  
- ==**Tagged Ports ("Trunk Ports")** carry traffic for multiple VLAN's with the VLAN tag preserved to identify traffic. Usually used for inter-switch connections or for VLAN aware devices, and can use filtering to decide which VLANs allowed to transverse link.==


==They have no security properties, any who access / reconfigure switch can see all packets.==

Ultimate combination is Link Agg + VLAN, so sending 2 or more networks over 2 or more cables with full load balancing and fail over. So capable of sending data from multiple networks into 1 cable, and the VLAN tagging to separate that traffic.

### Load Balancing of systems

Load balancing ensures network traffic is distributed across multiple network resources , preventing any 1 server form becoming and improving performance

Used to be commonly done with DNS unfortunately, Treat 1 domain name as multiple IP addresses and clients would test to see which IP addresses were available.
Can have issues if clients has outdated cache, resulting in connecting to failed servers.

###### Modern Load Balancing
Now done with 1 IP address, balanced over multiple servers via Inbound NAT, constantly pinging to view live connections.
Dedicated load balancer manages traffic distribution in real time.

- **Distributed Algorithms used:** Round-robin, least-connections, weighted, etc.

Need slightly more beyond Inbound NAT to make it "stickier", routing frequent sources to usual destination, for purposes of cookies and sessions data etc,

###### Handling Server failures
If you need to view all traffic (Routers, Firewalls), it's difficult to load balance but for fail over, you can use **VRRP (Virtual Router Redundancy Protocol)**.

==Used for automatic gateway failover by creating virtual router with a virtual IP (VRID) between physical devices which is the advertised as real service address. There is a master node and backup nodes, with monitoring and take over when master is down.==

**Mechanism:**
- A group of devices share a **virtual IP**.
- One node is **MASTER**, others **BACKUP**, determined by priority.
- If MASTER fails, the highest-priority BACKUP takes over the virtual IP.

###### Full Architectures

- ==**Active/Passive Gateway Pairs**: VRRP-managed router pairs providing gateway redundancy==
- ==**Active/Active Load Balancer Clusters**: Distributing traffic across multiple load balancers==
- ==**Distributed Application Tiers**: Multiple application servers behind load balancers==
- ==**Geographic Redundancy**: Multiple data centres with any cast services for global resilience==

###### Design Considerations

- ==**Proper Monitoring**: Complete visibility into all system components==
- ==**Testing Regimes**: Regular failover testing to verify redundancy works as expected==
- ==**Data Synchronization**: Maintaining state consistency across redundant components==
- ==**Capacity Planning**: Ensuring N+1 or N+2 capacity for all critical services==

### Anycasting

**Anycasting** is a method of distributing network traffic globally by advertising the same IP prefix from multiple locations and routing each client to the **nearest (low-cost) instance**.

**Applications**:

- **UDP-based** services (DNS, NTP, many CDNs)—stateless or short-lived flows
- **Static content delivery** where connection migration isn’t needed.
- DNS services often rely on Anycasting to ensure fast and reliable name resolution worldwide.
- **Caveat for TCP:** Long-lived sessions may break if BGP path changes mid-session.


##### References


----
[Net-Lecture12-Multiple-IP](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_11/Net-Lecture12-Multiple-IP.pdf)

![[Net-Lecture12-Multiple-IP 1.pdf]]