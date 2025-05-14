2025-02-15 14:04

Status:

Tags: [[Dependable and Distributed Systems]]

---
Requirements:

- technical coverage
- critical analysis
- source selection
- organisation (structure essentially)
- document quality

**Structure:**

- Introduction - topic area and how review is broken down in to themes
- Themes - Each of the main ideas you want to talk about presented by the different sources, narrowing down to the main point of the research. Each theme will end with a summary of the overview of a theme
- Conclusion - 


**Topic:**

Leaning towards writing about how secure, reliable connections between devices underwater communicate and share information from water <--> water, water <--> Ground, water <-->Sky , and how depths, and limitation of chosen technologies effect the performance or possibility of these communications. Should include modern implementations of this and limitations.

Should include error handling, duplicates, performance of communication etc.

Themes

Structure

**Main topic: Maintaining high performance channels in underwater acoustic networks between underwater sensors**

Introduction: Discuss the necessity of the issue, stating why this is used, the practical applications of it and it's benefits, how it used to be done in the past, and a general where we are today in terms of handling the underwater acoustic networks

Themes:
- Factors effecting the performance of underwater acoustic networks
- Performance of underwater acoustic networks and how they are affected
- Protocols and algorithms to maintain throughput
- Design/topologies of decentralised underwater acoustic networks and their dimensions  

Conclusion: Gone over the current state of underwater acoustic networks, in terms of where the technology comes to today, limitations/challenges still yet faced, and plans for the future to overcome some said challenges
## **Synthesis Matrix**

Each theme will have it's own matrix, the way it works being each source will have multiple main ideas that can come under that theme, deriving that idea and information supporting it. Then for the next source, main ideas again, if it's the same main ideas, add it to the same row, otherwise add a new row for this new main idea. So you'll have a large matrix with multiple gaps but also multi perspectives on this same idea, even if they are just confirming each other.


Example

Title: **Maintaining high performance channels in underwater acoustic networks between underwater sensors**

Introduction to introduce the topic


Introduction (200-300 words):
- Explore the different uses of unmanned devices and underwater networks, both in terms of their history and their necessity (so applications and benefits).
- Briefly mention the recent changes and additional improvements to the field.
- Mention the main challenges found with underwater networks and how they compare to networks on the surface, such as why acoustic networks are used and what problems are introduced then
- Go over what the rest of the literature review will be going over in terms of themes, that being want to cover, that being the different issues affecting those networks, techniques and implementations to get around them, followed by a real example of underwater acoustic networks.

Theme 1 (400-500 words): Factors effecting the performance of underwater acoustic networks

- Want to mention how acoustic networks work in comparison to electromagnetic on the surface and the main issues that causes such as latency, high package lost, low bandwidth of data, signal fading, multipath propagation.
- Mention how data is sent across in underwater networks to
- Make clear the fundamental limitations of this communication method in terms of speed, power management, repair etc,

Theme 2 (400-500 words): Protocols and algorithms to maintain throughput

- Mention routing and how packages are sent across networks
- Mention how faults such as package lost, duplication, low bandwidth is handled
- Compare it to TCP/IP addresses in how they handle and send data, both via similarities and differences. As well as unique challenges that come from underwater acoustic networks
- Give an example of performance and throughput as well as how faults are handled.

Theme 3: (400-500 words) - Design of system Protocols and algorithms to maintain throughput

- Mention how data is sent across in underwater networks to a surface buoys or ship to be sent across the wider surface area

*Theme 4: Algorithms and protocols to maintain throughput*

Many protocols and algorithms used in UWN overlap with traditional networks such as TCP/IP although there are significant differences. Both systems allow for retransmissions of erroneous packets [6] via send ACK's or Acknowledgements or implementing a time out system, where if responses don't occur in a "reasonable" time.

Of course, the time out length in UWA systems is significantly longer in comparison, and algorithms such as "fast retransmission" [8] where a packet is retransmitted if the sender receives 3 duplicate ACK's. UWN wouldn't be fast enough to make good use of this and sending duplicate packets in general is very power inefficient.

----

To overcome these limitations, underwater networks have incorporated advanced error control and interference mitigation strategies. Forward error correction (FEC) methods—such as Reed-Solomon codes, convolutional codes, or low-density parity-check (LDPC) codes—enable the receiver to correct errors on the fly, thereby reducing the need for energy-expensive retransmissions. In addition, adaptive modulation and coding (AMC) techniques allow the system to adjust transmission parameters (such as modulation order and coding rate) in real time based on the prevailing channel conditions. These dynamic adjustments help maintain a balance between high data throughput and robust error correction.

Interference and multipath effects are addressed through techniques like spread spectrum, beamforming, and multi-user detection, which are critical for minimizing the impact of environmental noise and overlapping signals in the challenging underwater acoustic channel [8].

----


Error and corruption of packets due to interference and multipath propagation must also be considered during the design, through such strategies such as Forward error correction (FEC) methods Methods and adaptive modulation and coding(AMC).
Both protocols are relatively simple, whether it be ensuring a receiver or relay, correct any errors found with packets before handling them further or adjusting transmission parameters such as rates and frequency used based on channel conditions. These dynamic real-time adjustments, help minimise likelihood of failure and therefore, necessity of retransmission, heavily increasing throughput.







*Theme 5: Measuring Bit rate and Power Usage of UWN in a multi hop network*
- Brief overview of the factors necessary for measuring performance in Hop network
- How it is typically measured in terms of the theory
- Example equation and performance metrics


---




Conclusion (200 words):

- Brief overview of what we've learnt throughout this literature review regarding underwater acoustic networks
- Mention briefly what recent technologies are on the horizon to help networks in regards to some of the issues presented


Despite being there since the beginning, and covering 71% of the earth's surface, humanity has only a explored and charted 5% of it. This is especially surprising since there's almost no land on earth human's have not set foot on. Marine life, resources and resevoirs, layout of the ocean floor has been for mostly been out of reach for must of human history, but with the invention of submarines and UAV's we finally have accecss to this valuable data.

Underwater sensor networks especially work 

Hence with after the first


##### References
----
