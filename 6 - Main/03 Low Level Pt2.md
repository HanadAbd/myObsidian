2025-01-08 15:30

Status:

Tags: [[Advanced Networking]]

---
WAN and LAN
---

Initially, WAN and LAN were considered for different purposes because of their different setups, although recently, the line is more blurred. LAN simply connected all the devices to a network and assigned each device a unstructured random number (that should be unique from other devices), and then just flooded the network with data and said "this is for B". Every device on the network would be able to read it, but usually only B would bother. They could then setup up a longer lasting connection between the two but that wasn't really necessary either.

For WAN, this isn't really possible, since you can't globally flood some data and say "this is for B". Hence the necessity for random but structured distinct ID's like ipv4 and more complicated and nuanced protocols for sending data across.

LAN quickly became faster with things like ethernet cables

Ethernet
---

Named after "luminiferous aether" which was a outdated theory on light needing a medium like sound needs air to travel.  The aether was this medium. Ethernet works in a similar way by having a large cable lots of devices are connected to, and they can just send data to the entire cable, saying who it was for, and that was it. Kind of like radio broadcasts but if everyone was on the same frequency.

Original topology is a bus.

---
### Format of packet/frame sent with Ethernet:

Most important things are the 
- 7 bytes of Preamble - string of 0x01010101 that's used to sync the clock of the reader to that of the transmitter since they might not match
- 4 bytes source MAC Address
- 4 bytes destination MAC Address
- 42-1500 bytes of payload
- 2 bytes of length/type, where if it's <=1500 bytes, return length, otherwise return type
- 4 bytes Cyclic Redundancy Check (CRC) which is just the checksum which you can can calculate after reading the rest of the packet
- 12 byte inter packet gap.

You can use either the inter packet gap or a calculation of all the data + the CRC to get the constant `0xC704DD7B`, to know you've reached the end of the frame.

---
So the main issue with this was, only one 1 station could talk at a time (since multiple transmissions will interfere with each other). Meaning handling collisions is an extremely complicated problem. ==Set of all stations whose packets may collide is called the **Collision Domain**==

Typically collision is handled by listening to the network at the same time of transmitting data. If it compares what it's listening to, to the  data being sent, and if there's a mismatch, someone is probably also talking. 

==All packets must be 64 bytes (or padded with 1 and 0 to be 64 bytes) so it will still have time near end of packet sent, you can send a set pattern of alternating 1 and 0 to ruin any checksums and make clear their is a collision.==

==64 value is a function of the maximum diameter of a collision domain (1500m).==

We then just flood the network to say there is a collision happening. Also ruins the checksum of any data on a network in order to ensure data is resent since it has been interfered with

Critical whole ethernet knows about collision before packet is received.
.

There's a protocol for resending data based on trying 10 times at different almost random times (doesn't need to be entirely random, just different then other devices). After 10 times, just gives up

This constant collision checking and resending makes it very unpredictable so latency is incredibly hard to predict since it also scales with traffic mix.

Maximum frame size is 1500 bytes, with minimum being 64.

Typically called "10base5" since it gave 10Mbps for 500m. Maximum being 1500m with 3 repeaters.



Hubs/Repeaters/Bridges
--

You can use elements to expand networks by connecting sub networks to each other. 
Repeaters just duplicate the signals from 1 to the other, essentially just expanding the network. That means all machines can see everything and can collide every where

A poor bridge might just check for collisions , and if everything is fine, send the frame of data. No collisions are passed 

Ideally bridge should do this but also look at the destination to pass data to the sides relevant for that frame
![[Pasted image 20241111164105.png]]
Ethernet Hubs are just a boxes of repeaters, collisions are carried over from the other side 

Switches
--

Basically a box full of bridges. Each station has is it's own gigabit connection to the switch, with the switch reading the header and sending it to the correct next station. Also incorporates "Full Duplex" which just means having 2 separate collision domains for in and out so collisions can't occur. Buffers on the switch handle storing data when cable is busy and sending it when it's not.


### ==Cut-Through Switches==

==We can do conservative switching (store and forward), and read the entire packet of data and confirming checksum before passing on to the destination, or we could do aggressive switching (cut through) and just read the header and immediately start transmitting before the whole frame has been received which reduces latency, but since it doesn't make it to the checksum, it can continue broken frames.==
Tokens
--

Alternatives to ethernet was tokens, where stations with the token could send data out and then a token is passed to someone else.

Very hard to get right however due to token loss and station failure. If a station with a token leaves the network, do every station make a token?

1 Alternative was slotted rings, so instead of tokens, have a long list of fixed empty frames, that stations could pass data to , say where it needed to go and then that station would pick it up.
![[Pasted image sds.png]]

Issues where what if it was never picked up, meaning some frames would be constantly taken (so requires complex algorithm for that) and also since it has  a minimum length, ends up with lots of extra cable and wasted space.

ATM
--
ATM (Asynchronous transfer mode) is a networking technology used that send fixed sized packets (called "cells") that are 53 bytes long. 5 for header, 48 for data. It is virtual circuit oriented by building a connection from source to destination and passing data over.

48 is not ideal since too high a number, reduces the data per second rate which can introduce echoes (interferences of the data caused by reflections) and therefore require echo cancellation.

There's ATM25 (for 25Mpbs) and faster alternatives like ATM155/622 but these still are in general losing out to Ethernet.

Since ATM switches couldn't handle the volume of circuit establishment required, permanent circuits are used instead.

Traffic Engineering
--

ATM leads to traffic engineering or policies to fairly manage how data is passed into VC's to be handled fairly in a limited bandwidth.

We can have different "profiles" by putting all data into a large buffer and sending it out according to the profile, although we do have to be conscious of data loss when buffer is full, causing packets to be dropped and needing to be resent.

"Profiles" can include:
- Constant bit rate -  fixed speed of data sent from point to point
- Variable bit rate- Allows you to burst higher speeds
- Available bit rate -  minimum bit rate but potentially delays packets that exceed it
- Unspecified bit rate: best effort of rate, delay reliability

All guaranteed to be ordered.

WDM (Wave division Multiplexing)
--

Uses **frequency domain multiplexing** to use different colour lights to transmit multiple streams down the same path, with minimal nm difference in frequency between adjacent channels. Can carry different traffic for each channel, e.g. ATM or ether for ethernet which is most common.



• In 2023: 
-  Short range: ether over copper 
- Medium range and/or hostile environments: ether over multimode fibre (an optical fibre that allows multiple light modes which are just paths)
- Long range: ether over WDM


Single mode refers to only 1 path like for WDM and multimode is multi paths


Issues with switches
--

Rare nowadays do to how efficient they are but there are things worth considering like 

1. Capacity planning- need to plan how fast switches and ethernet have to be to manage peak times, what's going to be used on the network typically (streaming, sending files to server etc.)
   
2. **Queuing** refers to the temporary storage of packets in switch buffer when  network is congested or when the output port cannot handle the incoming data fast enough. It helps manage burst traffic and smooth out transmission rates over time. The switch's buffer is used to hold these packets until they can be forwarded to their destination.
   
   **Buffer overflow** occurs when the switch's buffer becomes full because more data is being received than can be transmitted. When this happens, the switch will **drop packets** if there’s no space left. This can lead to **packet loss**.
   
   If a protocol like **TCP** is in use, the sender will notice the dropped packets and **retransmit** them. If **UDP** is used, the packets will simply be lost unless handled by the application.
   
3. Blocking - Backplane is the internal circuit that passes data to ports in the switch. If the sum of full bandwidth of all ports exceeds the back plane e.g. (24 1 Gbps ports so 48 Gbps full duplex but back plane is 32Gbps), then blocking occurs with packets either being dropped or buffered, leading to increase in latency.x
   
   
All hard to debug

Leaky bucket vs Random early dropping
--

We can have traffic shaping on the edge switches and traffic policing on the core switches. Leaky bucket just refers to the edge switches having a buffer (the bucket) that it puts data into and takes it out when sending. Any data that overflows the bucket is lost and needs to be resent. So everything will look fine up until 1 byte of space left. When full, packages will be lost at great speed causing real large gaps of data being sent in traffic bursts.

Hence random early droppings which tries to signify to the clients to slow down at given intervals (such as dropping 1% of packets at 50% bucket full) in order to get them not fill the bucket as quickly, and "flatten traffic".


Switches nowadays
--

Typically have a **core** switch which is connected to multiple **edge** switches, with core being the central hub that data is passed through and the edges being the actual connections to the clients.

Edges have deep buffers and is assumed to have a port for at least each client connected to it. 
Using 10GigE interconnects to the core switch which should have shallower buffers since handling data flow should be managed by the edge switches.
There is a full duplex GigE connection between edge and client and core to core connections. 



##### References


----
[Part 3 PDF](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Week_3/03%20Lower%20Layers%20-%20Part%20Two.pdf)

![[03 Lower Layers - Part Two.pdf]]