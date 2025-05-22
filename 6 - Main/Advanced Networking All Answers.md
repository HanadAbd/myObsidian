2025-05-14 22:41

Status:

Tags:

---
## Network Fundamentals

### 1. DoD (TCP/IP) Model vs. OSI Model [10 marks]

3 marks for correctly identifying and describing the layers of both models (OSI: Physical, Data Link, Network, Transport, Session, Presentation, Application; DoD: Link/Physical, Internet, Transport, Application).

3 marks for explaining key differences (OSI is theoretical with seven distinct layers, DoD is practical with four more functional layers, OSI was developed before widespread Internet adoption, DoD developed alongside actual Internet protocols).

3 marks for explaining why DoD is more practical (simpler structure, maps better to how protocols are actually implemented, developed with real-world networking in mind, fewer layers means cleaner interfaces).

1 mark for appropriate examples showing how protocols map to the models (HTTP/FTP in application layer, TCP/UDP in transport layer, IP in internet layer, Ethernet in link layer).
### 2. Packet Switching vs. Circuit Switching [8 marks]

2 marks for clear definitions of packet and circuit switching.

3 marks for explaining three specific advantages (1 mark each):

- Time domain multiplexing capability
- Ability to reroute around failed network elements
- More efficient resource utilization

3 marks for relevant examples demonstrating these advantages in practical networking scenarios.

## Lower Layers

### 1. Conservative vs. Aggressive Switching [6 marks]

2 marks for describing store-and-forward switching (receives entire frame before forwarding, checks for errors).

2 marks for describing cut-through switching (begins forwarding after reading destination address, without waiting for entire frame).

1 mark for analysis of tradeoffs (latency benefits vs. potential error propagation).

1 mark for identifying appropriate scenarios for each approach.

### 2. Traffic Shaping and Policing [8 marks]

2 marks for explaining traffic engineering concepts and why they're needed.

2 marks for describing the leaky bucket approach (constant output rate from buffer).

2 marks for describing random early dropping (probabilistic dropping at defined thresholds).

2 marks for explaining how these mechanisms prevent buffer overflow and improve network performance.

## IP

### 1. IPv4 Fragmentation and Path MTU Discovery [10 marks]

3 marks for explaining the IPv4 fragmentation mechanism (identification field, flags, fragment offset).

2 marks for identifying problems with fragmentation (inefficiency, end-to-end retransmission for lost fragments, security concerns).

3 marks for explaining Path MTU Discovery (testing with MF=1, ICMP "fragmentation needed" responses, caching path MTU).

2 marks for explaining IPv6's different approach (no intermediary fragmentation, sender-only fragmentation).

### 2. IPv4 Address Allocation Evolution [8 marks]

2 marks for explaining the class-based system (A, B, C classes and their address ranges).

2 marks for describing evolution to CIDR (variable-length subnet masks, collapse of class boundaries).

2 marks for explaining benefits of subnetting (more efficient address utilization, logical network segmentation).

2 marks for correctly providing a subnetting example for a Class C network (192.168.1.0/24 divided into four equal /26 subnets with correct address ranges).

### 3. ARP and IPv6 Neighbor Discovery [6 marks]

2 marks for explaining ARP operation ("who has this IP?" broadcast, response mechanism, caching).

2 marks for identifying security and performance concerns (broadcast traffic, spoofing/poisoning, no authentication).

2 marks for comparing with IPv6 Neighbor Discovery (multicast instead of broadcast, integrated into ICMPv6, additional functions beyond ARP).

## Address Allocation

### 1. DHCP vs. DHCPv6 vs. SLAAC [10 marks]

3 marks for explaining DHCP operation (DORA process, lease system, centralized control).

3 marks for comparing DHCPv6 and SLAAC (stateful vs. stateless, router advertisements, configuration options).

2 marks for analyzing security implications (rogue servers, privacy concerns with MAC-derived addresses).

2 marks for providing appropriate recommendations for different network types (enterprise vs. home vs. mobile).

### 2. DHCP Server Architecture Challenges [10 marks]

3 marks for explaining potential DHCP server issues (single point of failure, debugging difficulty, complex state management).

3 marks for explaining relay agent operation (unicast forwarding across networks, relay addressing).

3 marks for identifying security considerations (lease period configuration, rogue servers, address pool exhaustion).

1 mark for explaining enterprise-specific deployment considerations (centralization, redundancy).

## Multiple Interfaces

### 1. DNS-based vs. NAT-based Load Balancing [8 marks]

3 marks for comparing DNS-based and NAT-based approaches (multiple IP records vs. single IP distribution).

3 marks for explaining failure handling and health monitoring (TTL issues vs. real-time monitoring).

2 marks for discussing session persistence approaches (limited control vs. source tracking).

### 2. Virtual Router Redundancy Protocol (VRRP) [8 marks]

3 marks for explaining VRRP purpose and operation (virtual IP, prioritized master/backup).

3 marks for detailing the election process and failover mechanism (advertisement intervals, priority-based selection).

2 marks for discussing implementation considerations and benefits for high availability.

### 3. Virtual LANs (VLANs) [10 marks]

3 marks for explaining VLAN tagging (802.1Q frame format, 4-byte tag structure).

3 marks for distinguishing tagged and untagged ports (access vs. trunk ports, PVID assignment).

2 marks for explaining "router on a stick" configuration for inter-VLAN routing.

2 marks for identifying security considerations (lack of encryption, switch configuration protection).

## TCP and UDP

### 1. Selective Acknowledgement (SACK) [8 marks]

3 marks for explaining the three duplicate ACK scenario and how cumulative acknowledgement handles it.

3 marks for explaining how SACK differs (acknowledging blocks beyond gaps, SACK block format).

2 marks for discussing efficiency benefits (reduced retransmissions, improved recovery time).

### 2. TCP vs. UDP Demultiplexing [6 marks]

3 marks for explaining the demultiplexing processes of both protocols.

3 marks for explaining why TCP requires a 4-tuple while UDP can function with a 2-tuple.

### 3. Silly Window Syndrome [6 marks]

2 marks for explaining Silly Window Syndrome (small receive windows causing inefficient transmission).

2 marks for explaining the receiver-side approach (advertising only significant buffer space).

2 marks for explaining the sender-side approach (Nagle's Algorithm) and how it prevents the problem.

### 4. TCP Sliding Window and Window Scaling [10 marks]

3 marks for explaining sender and receiver window operation (flow control mechanism).

2 marks for explaining window size advertisement in TCP header.

3 marks for explaining window scaling option and its operation (scale factor, effective window calculation).

2 marks for explaining importance for high bandwidth-delay networks with relevant calculation.

## NAT and Unusual Transports

### 1. NAT Challenges and Solutions [10 marks]

6 marks for identifying and explaining four specific NAT challenges (1.5 marks each):

- Authentication and logging difficulties
- Protocol breakage for embedded addresses
- Port-pair exclusivity
- Peer-to-peer communication blocking

2 marks for explaining potential solutions or workarounds.

2 marks for explaining why NAT is only a temporary solution (end-to-end principle violation, complexity).

## HTTP

### 1. HTTP Performance Optimization [10 marks]

3 marks for explaining Keep-Alive and connection persistence.

2 marks for explaining content negotiation (Accept headers and server response selection).

2 marks for explaining caching mechanisms (directives, expiration).

3 marks for explaining ETag and Last-Modified conditional requests and their benefits.

### 2. HTTP vs. FTP [10 marks]

3 marks for comparing connection models (single vs. dual connection).

3 marks for comparing operational aspects (request/response vs. command/data channels).

2 marks for analyzing technical challenges (firewall compatibility, NAT traversal, file transfer mechanisms).

2 marks for explaining why HTTP has largely replaced FTP (simplicity, integration, security).

## DNS

### 1. DNS Resolution Process [8 marks]

3 marks for explaining the complete resolution steps from client to final IP address.

3 marks for identifying specific server roles in the process (stub resolver, recursive server, authoritative servers).

2 marks for detailing query exchanges and considering the Tokyo office location implications.

### 2. Recursive vs. Authoritative DNS Servers [8 marks]

3 marks for comparing server types and their functions.

3 marks for explaining interactions between server types in the resolution process.

2 marks for analyzing benefits of operating organization-owned recursive servers.

### 3. DNS Vulnerabilities and Mitigation [8 marks]

6 marks for identifying and explaining three specific vulnerabilities and their mitigations (2 marks each).

2 marks for providing infrastructure recommendations to maximize resilience.


## Older Questions

## Question 1: TCP/IP Protocol Evolution

### (a) High Bandwidth-Delay Product Problems [8 marks]

**Mark allocation:**

- 3 marks for explaining bandwidth-delay product concept and problems it causes
- 2 marks for identifying TCP limitations in the original standard
- 3 marks for correctly calculating maximum data rate

**Marking guidelines:**

- Full marks (7-8): Clear explanation of how high BDP affects window size requirements; identification of 16-bit window size limitation in original TCP; accurate calculation showing how 64KB window and 3000km distance limits throughput
- Good (5-6): Reasonable explanation of BDP issues; mention of window size limitation; calculation with minor errors
- Satisfactory (3-4): Basic understanding of BDP; incomplete explanation of TCP limitations; attempted calculation
- Poor (0-2): Minimal understanding of BDP concept; major errors in calculation; significant misunderstanding of TCP limitations

### (b) UDP Application Performance [8 marks]

**Mark allocation:**

- 2 marks for calculating single operation latency
- 2 marks for identifying assumptions about UDP operation
- 4 marks for suggesting approaches to achieve required performance

**Marking guidelines:**

- Full marks (7-8): Accurate latency calculation (20ms at light speed for 3000km); clear statement of reasonable assumptions; multiple sophisticated approaches for achieving 500 operations/second
- Good (5-6): Reasonable latency calculation; stated assumptions; some viable approaches suggested
- Satisfactory (3-4): Basic latency calculation with minor errors; limited assumptions; simple approach suggested
- Poor (0-2): Significant errors in calculation; missing or unreasonable assumptions; inadequate solutions

### (c) IPv4 Address Shortage [4 marks]

**Mark allocation:**

- 2 marks for explaining causes of IPv4 address shortage
- 2 marks for suggesting two valid expansion approaches

**Marking guidelines:**

- Full marks (4): Clear explanation of IPv4 limitations (32-bit address space, inefficient early allocation); two well-explained solutions (e.g., NAT, IPv6 adoption)
- Satisfactory (2-3): Basic understanding of address limitation; two solutions mentioned with limited explanation
- Poor (0-1): Minimal understanding of IPv4 limitations; inadequate or single solution proposed

## Question 2: TCP Transport Protocol

### (a) TCP Sliding Window [10 marks]

**Mark allocation:**

- 4 marks for explaining sliding window concept and operation
- 3 marks for sender-side operation description
- 3 marks for receiver-side operation description

**Marking guidelines:**

- Full marks (9-10): Comprehensive explanation of sliding window mechanism; detailed explanation of sender buffering, transmission, and window adjustment; thorough description of receiver buffering, in-order processing, and window advertisement
- Good (7-8): Clear explanation of sliding window; good description of both sender and receiver operations with minor omissions
- Satisfactory (5-6): Basic understanding of sliding window concept; adequate description of either sender or receiver operation
- Poor (0-4): Minimal understanding of sliding window; significant errors or omissions in describing operations

### (b) TCP Acknowledgement Mechanism [10 marks]

**Mark allocation:**

- 3 marks for explaining what data is acknowledged
- 3 marks for explaining when acknowledgements are sent
- 4 marks for comparing two acknowledgement strategies

**Marking guidelines:**

- Full marks (9-10): Thorough explanation of cumulative acknowledgment system; detailed description of acknowledgment timing strategies; comprehensive comparison of immediate vs. delayed ACKs with performance implications
- Good (7-8): Clear explanation of acknowledgment system; good description of timing options; reasonable comparison of strategies
- Satisfactory (5-6): Basic understanding of acknowledgments; some description of timing; limited comparison
- Poor (0-4): Minimal understanding of acknowledgment system; significant errors or omissions in descriptions

## Question 1: TCP and UDP Comparison

### (a) Reliable, Sequenced Delivery [4 marks]

**Mark allocation:**

- 2 marks for explaining "reliable, sequenced delivery"
- 2 marks for correctly identifying and explaining which protocol offers these properties

**Marking guidelines:**

- Full marks (4): Clear definition of reliability (guaranteed delivery, error detection/correction) and sequencing (maintaining order); correct identification of TCP as offering these properties with explanation
- Satisfactory (2-3): Basic definition of terms; correct identification with limited explanation
- Poor (0-1): Minimal or incorrect understanding of terms; incorrect identification

### (d) Latency in Wide-Area Networks [8 marks]

**Mark allocation:**

- 3 marks for explaining latency in WAN context
- 5 marks for analyzing how latency and reliability affect protocol choice

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of latency (propagation, transmission, queuing, processing); detailed analysis of how different application requirements influence protocol choice based on latency tolerance and reliability needs
- Good (5-6): Clear explanation of latency; good analysis of protocol choice factors
- Satisfactory (3-4): Basic understanding of latency; limited analysis of protocol choice
- Poor (0-2): Minimal understanding of latency; inadequate analysis of protocol choice

## Question 2: Domain Name System

### (a) DNS Record Types [5 marks]

**Mark allocation:**

- 1 mark for explaining AAAA record type
- 2 marks for each additional record type explained (2 types, 2 marks each)

**Marking guidelines:**

- Full marks (5): Clear explanation that AAAA records map domain names to IPv6 addresses; two additional record types (e.g., A, MX, CNAME, NS, TXT) with accurate purpose descriptions
- Good (3-4): Correct AAAA explanation; one additional type explained well or two with minor errors
- Satisfactory (2): Basic understanding of AAAA records; limited explanation of additional types
- Poor (0-1): Incorrect understanding of AAAA records; inadequate explanation of additional types

### (b) TTL in DNS Records [4 marks]

**Mark allocation:**

- 2 marks for explaining TTL purpose
- 2 marks for discussing benefits/drawbacks of different TTL values

**Marking guidelines:**

- Full marks (4): Clear explanation that TTL controls how long records can be cached; comprehensive discussion of short TTLs (faster propagation, higher load) vs. long TTLs (better caching, slower changes)
- Satisfactory (2-3): Basic explanation of TTL; some discussion of different values
- Poor (0-1): Minimal understanding of TTL; inadequate discussion of implications

### (c) Recursive DNS Resolution [3 marks]

**Mark allocation:**

- 3 marks for explaining recursive resolution process

**Marking guidelines:**

- Full marks (3): Clear explanation of the recursive resolution process starting with root servers, then TLD servers, then authoritative servers for google.com
- Satisfactory (2): Basic explanation with minor errors or omissions
- Poor (0-1): Significant errors or omissions in explaining resolution process

### (d) DNS Replacement Design [8 marks]

**Mark allocation:**

- 3 marks for architecture outline
- 5 marks for addressing specific DNS problems

**Marking guidelines:**

- Full marks (7-8): Comprehensive architecture design; addresses multiple DNS problems (security, performance, scalability) with viable technical solutions
- Good (5-6): Reasonable architecture design; addresses some key DNS problems
- Satisfactory (3-4): Basic architecture with limited problem-solving
- Poor (0-2): Inadequate architecture; fails to address significant DNS problems

## Question 3: Address Allocation

### (a) Static, DHCP, and SLAAC Comparison [8 marks]

**Mark allocation:**

- 5 marks for comparing the three address allocation methods
- 3 marks for justifying preferred solution for consumer IPv6 networks

**Marking guidelines:**

- Full marks (7-8): Comprehensive comparison of all three methods (advantages, disadvantages, operation); well-reasoned preference for consumer IPv6 networks (likely SLAAC) with consideration of usability, management, and privacy
- Good (5-6): Good comparison of methods; reasonable justification for preference
- Satisfactory (3-4): Basic comparison; limited justification for preference
- Poor (0-2): Inadequate comparison; unjustified or incorrect preference

### (b) Subnetting Concept and Application [4 marks]

**Mark allocation:**

- 2 marks for explaining subnetting concept
- 2 marks for suggesting allocation approach for given scenario

**Marking guidelines:**

- Full marks (4): Clear explanation of subnetting (dividing address space into smaller networks); viable approach for allocating 147.188.0.0/16 to hundred units (e.g., using /24 for each unit)
- Satisfactory (2-3): Basic understanding of subnetting; partially correct allocation approach
- Poor (0-1): Minimal understanding of subnetting; inadequate allocation approach

### (c) DHCP Infrastructure Design [8 marks]

**Mark allocation:**

- 8 marks for comprehensive DHCP infrastructure design

**Marking guidelines:**

- Full marks (7-8): Sophisticated design addressing redundancy (primary/secondary servers), synchronization, lease duration, and specific strategies for preventing duplicates during reconnection
- Good (5-6): Reasonable design addressing most key concerns
- Satisfactory (3-4): Basic design with limited consideration of failure scenarios
- Poor (0-2): Inadequate design failing to address duplicate prevention

## Question 1: Ethernet

### (a) Ethernet Collision Detection [6 marks]

**Mark allocation:**

- 6 marks for describing collision detection mechanism

**Marking guidelines:**

- Full marks (5-6): Comprehensive explanation of CSMA/CD, including listening while transmitting, signal comparison, collision detection, jam signal, and backoff algorithm
- Good (3-4): Clear explanation with minor omissions
- Poor (0-2): Significant errors or omissions in describing collision detection

### (b) Switched and Full-Duplex Advantages [6 marks]

**Mark allocation:**

- 3 marks for switched operation advantages
- 3 marks for full-duplex operation advantages

**Marking guidelines:**

- Full marks (5-6): Comprehensive explanation of switched advantages (separate collision domains, filtering) and full-duplex advantages (simultaneous transmission/reception, elimination of collisions)
- Good (3-4): Clear explanation of most advantages with minor omissions
- Poor (0-2): Significant errors or omissions in describing advantages

### (c) Virtual LANs [8 marks]

**Mark allocation:**

- 3 marks for describing VLAN operation
- 3 marks for describing an application with clear advantages
- 2 marks for details of operation, security considerations, etc.

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of VLAN operation (802.1Q tagging, switch configuration); excellent application example with clear benefits; additional details on security or implementation
- Good (5-6): Clear explanation of operation; reasonable application example
- Satisfactory (3-4): Basic explanation of VLANs; limited application example
- Poor (0-2): Minimal understanding of VLAN operation; inadequate application example

## Question 2: IPv4 Address Space

### (a) IPv4 Address Shortage [4 marks]

**Mark allocation:**

- 4 marks for explaining IPv4 address shortage causes

**Marking guidelines:**

- Full marks (4): Comprehensive explanation including 32-bit limitation (4.3 billion addresses), inefficient early allocation practices, growth of Internet-connected devices, and address class inefficiencies
- Satisfactory (2-3): Basic explanation of key factors
- Poor (0-1): Minimal understanding of address shortage causes

### (b) Network Address Translation [12 marks]

**Mark allocation:**

- 4 marks for explaining NAT function and basic operation
- 4 marks for explaining TCP traffic handling
- 4 marks for explaining UDP traffic handling

**Marking guidelines:**

- Full marks (10-12): Comprehensive explanation of NAT purpose and operation; detailed explanation of TCP handling (connection tracking, header rewriting); thorough explanation of UDP handling (temporary mappings, timeout-based state)
- Good (7-9): Clear explanation of NAT purpose; good description of TCP and UDP handling with minor omissions
- Satisfactory (4-6): Basic understanding of NAT; limited explanation of protocol handling
- Poor (0-3): Minimal understanding of NAT; significant errors in protocol handling explanation

### (c) IPv6 and Address Allocation [4 marks]

**Mark allocation:**

- 2 marks for explaining IPv6 elimination of NAT need
- 2 marks for explaining two IPv6 address allocation mechanisms

**Marking guidelines:**

- Full marks (4): Clear explanation of how IPv6's vast address space eliminates NAT requirement; accurate description of two allocation mechanisms (DHCPv6 and SLAAC)
- Satisfactory (2-3): Basic explanation of IPv6 advantages; limited description of allocation methods
- Poor (0-1): Minimal understanding of IPv6 benefits; inadequate description of allocation methods

## Question 3: TCP and UDP

### (a) Reliable and Sequenced Meaning [4 marks]

**Mark allocation:**

- 2 marks for explaining "reliable" through TCP/UDP contrast
- 2 marks for explaining "sequenced" through TCP/UDP contrast

**Marking guidelines:**

- Full marks (4): Clear contrast showing TCP's reliability mechanisms (acknowledgments, retransmission) vs. UDP's lack thereof; clear explanation of TCP's sequence numbers maintaining order vs. UDP's absence of ordering guarantees
- Satisfactory (2-3): Basic contrast of protocols with some explanation of terms
- Poor (0-1): Minimal understanding of terms; inadequate contrast

### (b) TCP Mechanisms [8 marks]

**Mark allocation:**

- 4 marks for explaining cumulative acknowledgments
- 4 marks for explaining receive window operation

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of cumulative acknowledgments (acknowledging all data up to point); detailed explanation of receive window (flow control mechanism, buffer size advertisement)
- Good (5-6): Clear explanation of both mechanisms with minor omissions
- Satisfactory (3-4): Basic understanding of the mechanisms
- Poor (0-2): Minimal understanding of mechanisms; significant errors or omissions

### (c) TCP Out-of-Order Packet Handling [8 marks]

**Mark allocation:**

- 4 marks for explaining receiver processing of out-of-order packets
- 4 marks for explaining sender interpretation and fast retransmit mechanism

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of duplicate ACK generation for out-of-order packets; detailed explanation of fast retransmit when sender receives three duplicate ACKs
- Good (5-6): Clear explanation of process with minor omissions
- Satisfactory (3-4): Basic understanding of the process
- Poor (0-2): Minimal understanding; significant errors or omissions

## Question 4: Domain Name Service

### (a) DNS Server Types [4 marks]

**Mark allocation:**

- 4 marks for explaining distinction between server types

**Marking guidelines:**

- Full marks (4): Clear distinction between resolvers (client software), recursive servers (perform full resolution on behalf of clients), and authoritative servers (provide definitive answers for zones)
- Satisfactory (2-3): Basic distinction between server types with some confusion
- Poor (0-1): Minimal understanding of server types; significant confusion between roles

### (b) DNS Resolution Flow [8 marks]

**Mark allocation:**

- 8 marks for explaining DNS packet flow during resolution

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of all query stages from client to stub resolver to recursive server to root/TLD/authoritative servers, with specific packet exchanges described
- Good (5-6): Clear explanation of main query stages with minor omissions
- Satisfactory (3-4): Basic understanding of resolution flow
- Poor (0-2): Minimal understanding; significant errors or omissions

### (c) DNS Caching Mechanism [8 marks]

**Mark allocation:**

- 3 marks for explaining TTL mechanism
- 5 marks for analyzing implications of different TTL values

**Marking guidelines:**

- Full marks (7-8): Comprehensive explanation of TTL as cache duration control; detailed analysis of short TTL implications (faster propagation, higher query load) vs. long TTL implications (better caching, slower changes, potential staleness)
- Good (5-6): Clear explanation of TTL mechanism; good analysis of implications
- Satisfactory (3-4): Basic understanding of TTL; limited analysis of implications
- Poor (0-2): Minimal understanding of caching; inadequate analysis of implications



##### References
----
