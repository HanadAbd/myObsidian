2024-11-21 12:54

Status:

Tags: [[Advanced Networking]]

# UDP RFC 768

UDP (User Datagram Protocol) is a datagram transaction based protocol, that offers no guarantee of sequencing or data arriving. If those are needed TCP (Transaction Control Protocol).
Datagram since no connection is actually built, a packet with the relevant data/ header are just sent to a destination. Path they take could change.


![[Pasted image 20241121131431.webp]]

8 byte header.
2 byte Source Port isn't strictly necessary, and defaults to 0 if not used, but could also be used to state where replies should be sent
2 byte Destination Port is where it goes.
2 byte Length is the length of the entire packet, so header + data
2 bytes for checksum and uses the same procedure for TCP.

#### Checksum Procedure

Used for validating packets of data sent. Adds the binary of the pseudo header, UDP header and payload, to create a unique checksum and **then** flips all the bits. This is the checksum sent with the package

The pseudo header being data from the IP header in UDP/IP (e.g. source address, destination address etc.), and of course the UDP header for this calculation is set as 0.

The same calculation is done **but without flipping the bits**. It then adds the received checksum against there's and if it doesn't equal 0xFFFF, then that means the data is corrupted.

Most commonly used in DNS (Domain Name Server) and TFTP (Trivial File Transfer Protocol) which is light weight File Transfer Protocol.

##### References

https://datatracker.ietf.org/doc/html/rfc768

----
