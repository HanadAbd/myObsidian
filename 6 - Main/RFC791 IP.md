2025-01-08 12:26

Status:

Tags: [[Advanced Networking]]

---
This RFC describes the Internet protocol and how it works, explaining how it is called on by other transport protocols e.g. UDP/ TCP and is provided a destination address, source address and payload (along side other transport information).

Internet protocol works by "hopping" from network to network with the IP datagram containing all necessary information being sent to different networks and routers, who then reading and checking against their routing table, forward their data to either the final destination address or at least the closest prefix match in a different network. Sending it up the layers from local network back to the internet module as an IP datagram to go to the next network.





##### References


----
[RFC 791 Document](https://datatracker.ietf.org/doc/html/rfc791)