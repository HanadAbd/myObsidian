2025-01-19 11:20

Status:

Tags: [[Dependable and Distributed Systems]]

---
**Summary**:

This is book is about distributed algorithms, so algorithms that running on multiple different locations concurrently, whether that be different networks, processors, threads, etc. They can differ in how they share resources, synchronous or asynchronous, what problems they are being used to fix etc. 
Most importantly, due to how much is being done at once, ordering of processes, reading/writing, what process does what at what time, different speeds etc. can vary to the point of unpredictable, but the algorithm must be useful and work anyhow.

There are 3 different main model/ factors a distributed algorithm has:

- IPC (Inter process Communication) - How concurrent algorithms communicate with each other, e.g. a memory store, message passing via broadcasting etc.
- Timing module - So how these concurrent algorithms manage timing, synchronous, asynchronous, a mixture of both
- Failure Model - How these concurrent algorithms handle errors whether they be hardware, break down in communication, function etc.

*Chapter 2 , Modelling I: Synchronous Network Model (42): *


Uses the example of a network using a directed graph with the edges representing channels and each node have functions to send outgoing messages to neighbours and then clearing the channel.
Describes 3 hypothetical faliures:

- Halting: State for a node to be in 
- 





##### References
----
[Distributed Algorithms](file:///C:/Users/Asus/Downloads/Distributed%20Algorithms.pdf)