2025-05-02 15:57

Status:

Tags: [[Advanced Networking]]

---



## Introduction
TCP (Transport Control Protocol) and UDP (User Datagram Protocols) are both transport protocols that are both used in Internet Stack alongside the Internet Protocol to send data across applications. UDP is unreliable and unordered but extremely fast, used in older systems that couldn't afford the overhead of TCP. And TCP is reliable and ordered, and is the standard for sending streams data through a secure connection.


### Connection Demultiplexing

==This refers to demultiplexing in terms of sending data 1 after the other of time domain.== 


==Each TCP socket is identified by it's own 4-tuple (src and dest IP and Port) with a different socket for each connecting client.==

==IP address information is in the datagram, which a transport segment that contains port information.==

==For UDP, which is connectionless, use sockets with port numbers defined by dest IP address and Port number. So hosts checks UDP segment, looking at it's port number and directs segment to that port. So packets with same destination but different source information, will stay go to same socket which is messy.==  



---
## UDP
[[UDP RFC 768]]
But essentially the main benefits are smaller header size, no connection state needed, no connection establishment needed. Very fast and simple for older simpler systems

#### ==Checksum Procedure for UDP==

==Used for validating packets of data sent. Adds the binary of the IP header, UDP header and payload, to create a unique checksum and **then** flips all the bits. This is the checksum sent with the package==

==The same calculation is done **but without flipping the bits**. It then adds the received checksum against there's and if it doesn't equal 0xFFFF, then that means the data is corrupted.==



----
## TCP Problems

There are few issues that occur with TCP that it needs to handle
1. Packet is corrupted or has an error
2. Packet gets lost
3. Handling duplicates from retransmissions.
4. Latency can get really big with large distances

With each of these having their own sub problems.

For errors, if it is corrupted, you **might** be able to tell from the checksum and therefore instead of sending **ACK**, you can send **NACK** (negative acknowledgement)  to say it needs to resend the packet. But since a **NACK** can also get corrupted, whenever it **timeout** without receiving an acknowledgments, it just resends. Since each packet has a sequence, it just needs to consider 1 packet per sequence number (since it knows it's just a duplicate).

There's a **timeout** for each packet sent from the sender, so how long they are willing to wait for some acknowledgement before just sending it out

This sequence number can also be used for packets that get lost.

Due to latency however sending a packet and waiting for a response per packet would take too long  (e.g. 3000km would be 20ms at the speed of light for send + reply) so instead we can use a **pipeline** to send multiple packets that are yet to be acknowledged, with buffers on either side to store them.
![[Pasted image 20241122133626.webp|856]]

---
## TCP Piped Protocol

Send N un-acked packets in pipeline.
The sender has a sequence that it sending out
![[Pasted image 20241122135733.webp|856]]

So the sender is constantly sending packets, the receiver sends acknowledgements for each packet, until a packet is loss or corrupted. If so, it discards everything new being sent, and just resends the acknowledgements of the last valid packet.

For the sender when that missing packet **timeout**, it then sends everything past the missing packet including the missing packet. 

The alternative is **Selective Repeat**

Selective Repeat
---
==Selective Repeat is a standalone protocol typically used with RTP or implementations of UDP, using a per-block ACK system==

Instead of cumulative acknowledgement, so only acknowledging the last before a packet is lost, and refusing to acknowledge anything else until then, ==selective repeat simply acknowledges all correctly received packets==, and waits for the lost packet to timeout, at which point, it will be resent.

==Therefore sender timer for each unACKed Packet, instead of just 1.== 

Main advantage being, it allows the sender to buffer out out of order packets.



---
## TCP Structure

![[Pasted image 20241122141749.webp]]
- Same port system and checksum as UDP.
- Sequence number being for ordering packets and identifying packets.
- Receive windows, just specifies the size of the buffer for the receiver. So max is 64kb (since it's just 16bits) but ideally should be more for more advanced recent technology
- Acknowledgment number is to signify the next packet to be sent (so it asks for the next vaild packet in the sequence. If it is lost or errored, they just keep asking for the same thing).
  
  
- ACK - Used to signify whether Acknowledge number is valid for this packet
- Reset- Emergency close connection
- FIN - Ordered Complete close of connection

---
Bytes, not Packets

The sequence number and acknowledge number are considering it in bytes, not packets, since packages can range varying amounts of bytes and a single packet may not contain everything you want. 

![[Pasted image 20241122151331.webp|476]]

----
## Issue with Timeouts

Getting the perfect timeout can be really hard . By default, needs to longer then the varying **RTT** (Round Time Trip) since too short, we'll have lots of unnecessary retransmissions and duplicates, and  things that are slightly delayed are too late. But too long, and it becomes useless and slow, since it will be a long time until retransmission, so nothing happens until then.

Ideally, you can calculate the timeout from the last few ACK's sent to get a gauge of time+ a safety margin, just in case so it doesn't keep timing out when it shouldn't.

You can also just resend when you receive multiple duplicate ACK's (since that implies it really can't continue without it that packet so just start from back there again). It's standard for after receiving 3 duplicate ACK's to perform a fast retransmission, where you resent that packet without even waiting for it to time out.

Also only need to 1 timer for the last unacknowledged packet. And reset it for the next ACK. So no timer for every packet being sent


Better implementation of TCP
---

If you get data that you expect and this is constantly happening, you could just only send a ACK to cancel the timeout. So you can continue like that. Makes it easier for things like large file transfer where constantly sending out an ACK for every package probably isn't worth it.

Also could have a buffer at the receiver, so even if it receives data out of order, it can store it so just in case of the earlier packets were delayed (so can reorganise it on receiver side) or it's missing, in which case, ask for it, and then once you receive it, you can still re-organise it on your side.

But since the buffers in RAM aren't infinite, and we could have thousands upon thousands of TCP connections connected to a server for example, we have to limit and control the amount of buffer space offered. We could just offer a small amount of space, and if more is needed, it can be requested, or if it's not being used as often or efficiently, we can reduce the receiver buffer side for that connection. This is called **flow control** and with it, we shouldn't overflow the window size

Again, the implementation can be dependent on how stable the network even is.

Setting up connection
--
We need to set up connection, buffer, agree sequence numbers, and confirm there are clients on both ends

---
## TCP Options

Within the options section of the TCP header, we can add more options to "expand" what we can do with the protocol. If it is not recognised on both ends, it just ignored, and both sides continue like normal

Important Options include:
- Selective Acknowledgement
- Window Scaling
- Timestamping For PAWS

Algorithms Include:
- Slow Start
- Fast Re-transmission of dropped packets 
- Rapid Recovery to Slow Start

### Selective Acknowledgement (SACK)

Instead of cumulative acknowledgement, so sending acknowledgements for the last contiguous sequence of bytes received, e.g. 1,2,4 and 5 would lead to 2 duplicate ACK's of 2.

SACK does the same but give's more information by also passing a **SACK Block** to report _additional received ranges_ beyond the cumulative ACK. , e.g. ACK of 2 but also SACK Block of 4-5.**

Not as useful nowadays, especially with fast transmission.
[TODO CHECK THIS Definition against slide 71]

### Window Scaling

An almost default option with how popular is. Used to get around the receive window being 16 bit (so at most 64kb and we might have more available buffer space for this connection then just that) so instead we have an option with 3 bytes. First and second byte specify what option it is and it's total size 3 bytes. last byte gives a value from 1 to 14 called S which is the scale factor used against the window size to get up to `64Kb * 2^14 = 1GB`. So we can up all the way to 1 GB.

Does cause a potential problem of potentially going beyond the 4Gb sequence numbers, causing sequence numbers to wrapped. 
Solution is **PAWS (Protection against wrapped sequence numbers)** and just adds a timestamp, to help with ordering as you can distinguish against new and old packets. Also has the added benefit of giving us **RTTM (Round Trip Time Measurement)** which gives us the time it took for a packet to be sent and for us to get it's reply.

### Slow Start
 
Even if the receive window is large and plenty, sending all data at once that could fill up the window might overwhelm your local router, causing it to drop packages and causing a bottleneck with slower transfer.
To avoid this, the client will have it's own **congestion window** that is always equal or less then receive window to show how much data the client send "comfortably" before overflowing. It generates this congestion window, by sending 1 packet and doubling each time until window is full, easing congestion.

But there are different implementations for "ramping" up. Not as necessary nowadays since router memory isn't as large an issue


### Rapid Recovery / Fast Retransmit

Once many (at least 3) duplicate acknowledgements have been received, that packet will be resent (along with potentially the few packets ahead of it )without waiting for time out, keeping the **congestion window** partially full instead of resetting to 1 and going into **slow start**

### Timeout

When a Time out occurs, all **lost** packages are retransmitted with the assumption that it got lost. This might take a while and some might be needed sooner so those with 3 or more duplicate ACKs are **fast Retransmitted** so when time out occurs, only packets with 2 or less ACK's are retransmitted.


### ==Silly Window Syndrome==

==In the case of receive window being incredibly small e.g. 1 byte so sending message and ACK is incredibly inefficient, 2 different things can be done:==

- ==Receiver: Doesn't advertise small windows, only wheter you can accept more significant data e.g. half our buffer==
- ==Sender ("Nagle's Algorithm): Don't send small packets when there is outstanding unack'd data== 





##### References
----
[06 TCP and UDP](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_7/06%20TCP%20and%20UDP.pdf) 

![[06 TCP and UDP.pdf]]