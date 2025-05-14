2025-01-08 13:08

Status:

Tags: [[Advanced Networking]]

---
Mostly about factors that impact network performance and it's limitations.

### Factors about Bandwidth

Some factors are [[volume]] [[bandwidth]], [[latency]] and [[error rates]]. Volume or bandwidth just being the amount of bits per second. Latency being time taken for packet to arrive to destination and error rate being the error per gigabit.

Volume has increased a lot over the years but latency and error rates haven't as much. In fact error rates have increased.
This is because for latency, we're reaching the limit of the speed of light and error rates usually come from cosmic rays or connector issues, which only got worse when transistors became even smaller, so amount of energy needed to flip them decreased. so increased error rate.
Losing data isn't as bad since protocols can account for data not arriving, but verifying that the data that comes is correct is a lot harder.

What is important or isn't important depends on the use case. For a phone call, latency is very important so you can hear in real time, but data loss and low bandwidth rate isn't too big a deal, if it only amounts to a messier, low quality sound.

For file transfers however, seconds of latency aren't really an issue at all, but ensuring high data quality and loss of error is paramount. Especially if the data is massive.

### Packet / Circuit Switching

Instead of having a constant stream of data and everlasting connections even when no data is being sent, we send "Packets" of data. Data is broken down into packet sizes with a header that contains source IP and port, as well as destination port and IP. This data is sent to a switch that redirects the data to that destination if it is not as busy. If it is then it waits until it gets the chance. This is what has caused most of the bulk of latency.

##### ==Advantages of Packet switching against Circuit Switching==

- ==Incorporates multiplexing in the time domain.==
- ==Can reroute around failed switches for resilience==
- ==More resource efficient==

==Cons:==
- ==Packets can get lost, delayer or reordered==
- ==Might have to break larger data into packet, and re-combine on other end. So will need to wait for completed sequence.==
### Datagrams and virtual circuits

Datagrams do the typical packet approach of sending a packet with the information needed, which it sends to the switch which just routes into the destination.

Virtual circuits are a bit more involved since they set up a connection from source endpoint to destination endpoint through the switch and passes a token for that connection. All packets of data are sent through that connection until it's no longer necessary, and the connection is closed.


### Layering



A stack is just a way to view networks as a "stack" of interfaces that provide services to other layers. In principal, it just abstracts each layer from all the way from application to "wire" and passes data between them. Never needing to skip layers and only going 1 way.

==The OSI (Open Systems Interconnect) model was a failed stack for telecommunications. DoD mode/  TCP/IP suite is the modern equivalent and is a lot more simpler==

![[Pasted image 20241017115642.png]]

Each layer interacts with the lower layers, but never the layers above. They can be viewed as going from software all the way down to the bare bones hardware and wire. So you can view the order of events going from the Application Layer, down to physical, which connects to a router, which then connects you to the physical layer of the host, which we'll go back up to the application Layer. 

==For the DoD layer:==

Application layer is for the actual code and apps you're making. Protocols like HTTP, FTP (File Transfer Protocol) and other services are used by these applications to connect and get data from other machines.

Transport layer is for protocols like TCP and UDP that pass data to the endpoint of the machine. Usually combined with

using the internet layer which includes IP addresses, so interacting with that system of IPv4 and such. ==This moves packets across end systems==

And the final layers being link and physical, being the process of moving data from network element to another, and shifting bits over physical devices, so connecting ethernet cables across a network for example. ==Link is mecahnism for moving data e.g. WIFI or Ethernet.==


![[Pasted image 20241017121237.png]]



##### References


----


![[02 Lower Layers - Part One.pdf]]