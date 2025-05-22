2025-05-13 18:18

Status:

Tags: [[Advanced Networking]]

---
## New Questions
---

### Network Fundamentals
1. The DoD (TCP/IP) model has become the dominant networking model over the OSI model. Explain the key differences between these models and why the DoD model has proven more practical for Internet communications. Your answer should reference the specific layers of each model and their functions. [10 marks]
2. Compare packet switching with circuit switching, explaining three specific advantages of packet switching. Using examples from the provided notes, explain how these advantages improve network resilience and resource utilization. [8 marks]

Q) Compare packet switching with circuit switching, explaining three specific advantages of packet switching. Using examples from the provided notes, explain how these advantages improve network resilience and resource utilization. [8 marks]

A) Compare packet switching with circuit switching, explaining three specific advantages of packet switching. Using examples from the provided notes, explain how these advantages improve network resilience and resource utilization. [8 marks]

### Lower Layers

1. Compare conservative switching (store-and-forward) with aggressive switching (cut-through) in Ethernet networks. What are the tradeoffs in terms of latency, reliability, and error propagation? In what scenarios would each approach be preferred? [6 marks]
2. Explain the concepts of traffic shaping and policing in modern networks. Compare the "leaky bucket" approach with "random early dropping" for managing network congestion. How do these mechanisms help prevent buffer overflow problems? [8 marks]


### IP 

1. Fragmentation in IPv4 has been largely deprecated in modern networks. Explain the original mechanism of IP fragmentation, the problems it creates, and how Path MTU Discovery provides a more efficient alternative. Why does IPv6 take a fundamentally different approach to fragmentation? [10 marks]
2. Describe the evolution of IPv4 address allocation from the original class-based system to modern CIDR addressing. Explain how subnetting allows more efficient use of address space, and provide an example of how a Class C network (192.168.1.0/24) could be divided into four equal subnets. [8 marks]
3. Explain how ARP (Address Resolution Protocol) enables IP communication over Ethernet networks. What security and performance concerns exist with ARP, and how does IPv6's Neighbor Discovery Protocol differ in its approach? [6 marks]

### Address Allocation

1. Compare and contrast IPv4 DHCP with IPv6 address allocation methods (DHCPv6 and SLAAC). Analyze the security and management implications of each approach and provide recommendations for different network types. [10 marks]
2. DHCP server architecture presents several design challenges in complex networks. Explain the potential issues with DHCP servers and how they can be addressed using relay agents. What are the security considerations when deploying DHCP in an enterprise environment? [10 marks]


### Multiple Interfaces

1. Load balancing ensures efficient distribution of network traffic across multiple resources. Compare DNS-based load balancing with modern load-balancing techniques using inbound NAT. How do these approaches handle server failures and maintain session persistence? [8 marks]
2. Explain the operation of Virtual Router Redundancy Protocol (VRRP) and its role in providing high availability for gateway routers. Detail the election process between master and backup nodes, and how failover occurs when a master node becomes unavailable. [8 marks]
3. Virtual LANs (VLANs) allow multiple logical networks to exist on shared physical infrastructure. Explain how VLAN tagging works, the difference between tagged and untagged ports, and how a "router on a stick" configuration enables inter-VLAN communication. What security considerations should be addressed when implementing VLANs? [10 marks]

### TCP and UDP

1. During data transfer, the sender receives three duplicate acknowledgements for packet 45. Explain in detail how selective acknowledgement (SACK) would handle this situation differently from cumulative acknowledgement. Include in your answer the specific TCP header options used and how they improve efficiency. [8 marks]
2. Compare the demultiplexing processes for TCP and UDP. How does each protocol identify the correct application to deliver incoming data? Explain why TCP requires a 4-tuple (source IP, source port, destination IP, destination port) while UDP can function with less information. [6 marks]
3. The "Silly Window Syndrome" can significantly degrade TCP performance. Explain what causes this condition and the two approaches (receiver-side and sender-side) used to prevent it. How does Nagle's algorithm specifically address this issue? [6 marks]
4. TCP's sliding window mechanism is essential for flow control. Explain how the sender and receiver windows operate, how the window size is advertised, and how window scaling extends this mechanism for high bandwidth-delay product networks. Why is window scaling particularly important for modern high-speed networks? [10 marks]


### NAT and Unusual Transports

1. NAT creates several problems for modern network applications. Identify four specific challenges caused by NAT and explain potential solutions or workarounds for each. Why is NAT considered only a temporary solution to IPv4 address exhaustion rather than a long-term fix? [10 marks]


### HTTP

1. HTTP provides various mechanisms for optimizing performance and reducing server load. Explain how features like connection persistence (Keep-Alive), content negotiation, and caching work in HTTP. How do ETags and Last-Modified headers specifically help reduce unnecessary data transfers? [10 marks]
2. Compare HTTP to FTP in terms of their connection models and operation. Why has HTTP largely replaced FTP for many file transfer operations? Analyze how each protocol handles challenges like firewalls, NAT traversal, and file size determination. [10 marks]
### DNS 

1. Explain in detail the complete resolution process when a user in your Tokyo office attempts to access "[www.internal-app.company.com](http://www.internal-app.company.com/)" for the first time. Your answer should include all steps from the client's request to the final IP address being returned, identifying each type of DNS server involved and the specific queries exchanged. [8 marks]

2. Compare and contrast the roles and operations of recursive DNS servers and authoritative DNS servers. How do these server types interact during the resolution process? Why might an organization choose to operate its own recursive servers rather than rely on ISP-provided ones? [8 marks]
3. DNS is vulnerable to various forms of attack and failure. Identify three specific vulnerabilities in the DNS system and explain potential mitigation strategies for each. How might a large organization design its DNS infrastructure to maximize resilience against these threats? [8 marks]


## Old Questions
---


### **Question 1**

The TCP/IP protocol has evolved considerably since its initial specification nearly forty years ago. Several extensions were introduced to deal with the problems associated with networks with a high bandwidth-delay product, also known as "long fat networks", and there have been a range of solutions proposed to deal with the shortage of IPv4 addresses.

**(a)** Describe the problems which are caused by a high bandwidth-delay product. Which features in the TCP standard as originally designed make such networks problematic for high-performance networking? Assuming the speed of light is 3×1083×108 metres per second, calculate the maximum rate at which data can be sent between two computers 3000 kilometres apart using unextended TCP.  
[8 marks]

**(b)** Consider an application which has been written to use UDP for single-shot "query" and "response" operations. Considering the same 3000km separation, how long will each such operation take? State any assumptions that you make. If an application needs to reliably perform five hundred (500) such operations per second, what approaches might be used to allow this to work?  
[8 marks]

**(c)** There is a global shortage of IP version 4 addresses. Explain briefly the causes of this, and suggest two possible ways to expand the number of addresses available for allocation.  
[4 marks]

---

### **Question 2**

TCP is the dominant transport protocol used on today’s Internet.

**(a)** TCP uses the mechanism of a "sliding window" to manage reliable transmission and reception of data. The window defines the amount of unacknowledged data that is in flight. Explain the operation of the sliding window, with reference to the operation of both the sender and the receiver’s window. Your answer should include a description of how the sender processes data which applications pass down for transmission, and how the receiver processes arriving packets prior to passing data to an application.  
[10 marks]

**(b)** The operation of TCP relies heavily on the timely and efficient sending of acknowledgements to indicate the successful arrival of data. Explain the operation of TCP’s acknowledgement mechanism. What data is acknowledged, and when are those acknowledgements sent? When choosing an acknowledgement strategy, what are the implications for performance in terms both of efficiency and latency? Your answer should compare and contrast two alternative strategies.  
[10 marks]

---

### **Question 1**

The two main user-level protocols in the IP suite are TCP and UDP. They have different attributes. It is important to choose the correct one when designing an application.

**(a)** If a protocol is said to offer "reliable, sequenced delivery", what does this mean? Which of UDP and TCP offer this combination of properties? Briefly explain your answers.  
[4 marks]

**(d)** Explain the concept of "latency" in the context of a wide-area network. How do latency and reliability affect the choice of protocol used for an application? Refer to your answers in parts (b) and (c).  
[8 marks]

---

### **Question 2**

The Domain Name System (DNS) is a core component of the current Internet: it is the mechanism by which keys such as hostnames are mapped to values such as IP addresses. The DNS consists of a distributed database of resource records (often called RRs), for example:  
`google.com. 300 IN AAAA 2a00:1450:4009:815::200e`

**(a)** In the above example, AAAA is referred to as the record’s type. Explain the meaning of the AAAA type. Give two further types, and briefly explain their purpose.  
[5 marks]

**(b)** Again looking at the above examples, 300 is referred to as the record’s Time To Live, or TTL. Explain its use. Briefly discuss the benefits and drawbacks of using TTL values of 60 and 86400.  
[4 marks]

**(c)** A "recursive" DNS server is able to answer queries about any name on the connected Internet. Given this initial information:  
`. 51987 IN NS a.root-servers.net.`  
`a.root-servers.net. 77631 IN A 198.41.0.4`  
Briefly explain how a recursive server is able to translate `www.google.com` to an IP address.  
[3 marks]

**(d)** Your employer has been given the power to radically reshape the Internet overnight. You have been tasked with designing a replacement for the DNS to overcome its known security, performance and scalability problems, exploiting the vastly faster and more reliable computers of 2024. Outline an architecture and indicate where and how it solves existing problems with the DNS. You should write approximately one page.  
[8 marks]

---

### **Question 3**

A necessary task in networks is allocating addresses to devices.

**(a)** Compare and contrast the use of static addressing, DHCP and SLAAC. Which do you think is the preferred solution for consumer IPv6 networks? Justify your answer.  
[8 marks]

**(b)** Subnetting is often used to improve the allocation of larger allocations of addresses, particularly for IPv4. Explain the concept of subnetting, and suggest how it could be used to allocate addresses in `147.188.0.0/16` to a hundred units within an organisation.  
[4 marks]

**(c)** How would you design a DHCP infrastructure to ensure that addresses were handled correctly – in particular, avoiding duplicates – in the event of the link between the building breaking and reconnecting?  
[8 marks]


### **Question 1**

Ethernet is the dominant networking protocol of the 21st century.

**(a)** In the original 10Base2 and 10Base5 versions, Ethernet relied on collision detection to allow multiple stations to share one cable. Describe the mechanism of collision detection.  
[6 marks]

**(b)** Describe the advantages of (i) switched and (ii) full-duplex operation, as compared to 10Base2 and 10Base5 co-axial cable.  
[6 marks]

**(c)** Ethernet has been extended in recent years to include virtual LANs. Describe their operation, then describe one application where VLANs provide a clear advantage over other techniques.  
[8 marks]

---

### **Question 2**

IPv4 address space is in short supply.

**(a)** With reference to the size and allocation of IPv4 addresses, explain why there is a global shortage of addresses.  
[4 marks]

**(b)** Network Address Translation, or NAT, is the most common mechanism used to extend the life of IPv4 address space. Explain its function and how it operates for (i) TCP and (ii) UDP traffic.  
[12 marks]

**(c)** The long-term solution to IPv4 address exhaustion is IPv6. Describe how IPv6 eliminates the need for NAT, and explain two mechanisms by which IPv6 addresses are allocated within a particular LAN.  
[4 marks]
### **Question 3**

TCP is the dominant protocol for transferring data in a reliable, sequenced way. UDP is a simpler protocol which does not offer these properties.

**(a)** By contrasting TCP and UDP, explain the meaning of "reliable" and "sequenced".  
[4 marks]

**(b)** TCP uses "cumulative acknowledgements" and a "receive window" to transfer data. Explain the operation of these mechanisms.  
[8 marks]

**(c)** Although TCP does not feature negative acknowledgements, modern TCP stacks respond in a special way to the case where one packet in a sequence has not been delivered. Explain how this is done, and why it is a beneficial optimisation. You will need to discuss how the arrival of an out-of-order packet is processed by the receiver, and the way in which that response is interpreted by the sender.  
[8 marks]

---

### **Question 4**

The Domain Name Service offers, amongst other things, the ability to map hostnames to IP numbers and IP numbers back to hostnames.

**(a)** Explain the distinction between resolvers, recursive servers, and authoritative servers.  
[4 marks]

**(b)** Considering the case of resolving the name "[www.google.com](http://www.google.com/)", explain the flow of DNS packets as a client device makes a network connection to a specific address.  
[8 marks]

**(c)** The DNS relies heavily on caching. Explain the mechanism the DNS uses to limit the length of time data remains in the cache. What are the practical implications of using very short (of the order of seconds) or very long (of the order of weeks) values?  
[8 marks]



##### References
----
