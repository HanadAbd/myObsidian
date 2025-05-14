  2025-02-19 10:25

Status:

Tags: [[Dependable and Distributed Systems]]

---
Title: **Maintaining high performance wireless channels in underwater acoustic networks**

**1. Introduction:**
Despite being there since the beginning, and covering 71% of the earth’s surface [1] , humanity has only explored and charted 5% of it. This is especially surprising considering there is almost no land on earth that humans have not set foot on. Marine life, resources and reservoirs, and the layout of the ocean floor have, for most of human history, been out of reach; but with the invention of submarines and UAVs, we finally have access to this valuable data. Networks of underwater sensors have been used effectively in many areas of research—including ocean environmental observation and monitoring, mine reconnaissance, unmanned sensor applications, and even military applications such as tactical surveillance of foreign objects [2] .

However, despite great progress in this field, there remain numerous challenges in building underwater networks. These include tides, waves, interference from marine life, unwanted movement of nodes, and—most importantly—the dynamics of the ocean itself. Unlike the radio waves used in surface networks (which travel at light speed and can transmit vast amounts of data almost instantaneously), electromagnetic waves dissipate too quickly underwater to be useful beyond shallow depths [3] . Hence the need for acoustic communication—literal sound waves sent through the ocean—which introduces issues such as latency, dispersion, fading, environmental noise, attenuation, and necessitates a rethinking of data rate calculations used in traditional radio communication.

This review will cover how underwater acoustic networks (UWN) and acoustic communication in general work, the challenges inherent to the field, and the protocols and implementations used to mitigate these issues. It will then provide an overview of how these factors affect the final performance of UWNs.


**2. Factors effecting the performance of underwater acoustic networks**

Nodes in a UWN have "transducers" in order to receive and transmit data to it's connected nodes via channels called "acoustic links". Data itself is transferred via sound, with the range of frequencies defining the range of data which determines the data capacity of the channel. In these networks, data can be imagined as being sent via packets, similar to typical internet communication, with source and destination addresses. 

The key factors effecting UWN are:

- The high latency in comparison to traditional electromagnetic communication
- Environmental Noise, attenuation and reflections of sound via multi-propagation degrading signal strength and travel distance
- Difficulty with power consumption and repair

As mentioned in section 1, acoustic communication must be used in significant depths due to the physical limitations of electromagnetic communication. This comes with a great reduction of speed, with communication occurring at the speed of sound. Fortunately sound in sea water is much faster then on air, especially with the increase of depths, with speed scaling proportionally with  density as seen with the UNESCO equation [4], the standard measurement for density of sea water. For a given environment of 15 degrees, 35 ppt (35 grams per kg of sea water) and 0 bar, sound travels at 1507 m/s. This significantly lowers the bitrate due to how long it takes to travel.


![[Pasted image 20250220150302.webp|815]]

$$
\text{Fig. 1. Comparison of electromagnetic communication in comparison to acoustic communication[3]}
$$

Although speed increases, with depth, latency is still a fundamental issue for real-time system monitoring, but even then, depth can also enhance other issues. With multi path propagation, sound can reflect from nearby surfaces, whether it be the water/air barrier or nearby terrain causing delayed signals to overlap and interfere with each other, which is made worse by variations of speed due to depth. Another source of signal degradation comes simply from noise in the environment. Turbulence noises, shipping/shipping traffic, breaking waves, Thermal noise or even interference from transmissions from other nodes can interfere with signals.

Beyond these issues multi-path propagation, which would require solutions such adaptive equalization in the receiver to recover the bit stream from the received signal [5], another significant issue is just the environment. Fundamental, it's incredibly time cost consuming  to get underwater devices, even in a shallow network for repair and maintenance and especially power it. Devices at significant [6] depth require to be battery powered which typically requires coming up to the surface to be repowered which is far from efficient. 


**3 Design of system Protocols and algorithms to maintain throughput**


Initial UWN designs were simply connecting various devices via two way acoustic links and AUV's (Automated Unmanned Vehicles used to transfer resources between nodes), which is then connected a surface node in order to transfer data to other ground services via electromagnetic waves [7].

Although this centralised topology isn't the only option available, it does work well for tethered nodes, or nodes on a fixed dimension, either horizontal on the sea bed or vertical [2]. For fully fleshed 3d system, with unfixed sensors spanning large distances, a multi-hop topology is necessary, where nodes are only aware of and communicate with their nearest available neighbours they can safely pass messages too. Messages are then "hopped" from each node until they reach their source destination via the "shortest" path.

This multi-hop design raises two primary challenges:  **Reliable Data Transmission**, or the ensuring that data is sent safely from node to node in an environment where high latency, multipath propagation, and signal degradation are common. And **Dynamic Routing Efficiency**, or the Continuously recalculating routes to account for node mobility and environmental variations, while optimizing for factors such as distance, energy consumption, and transmission delay.

Without a centralised node, such as the surface buoy, there needs to be at least 1 master node who is relayed the position of each node within the system. This master node calculates the “cost” of various routing paths and continuously updates network routing information. Such dynamic routing not only compensates for potential link failures and drifting nodes but also adapts in real time to changing underwater conditions. In some advanced implementations, a hybrid approach is employed where centralized coordination for long-range communication is blended with decentralized, local routing decisions to minimize latency and packet loss while conserving power. Regardless, with a multi-hop topology, lot's of delay is inevitable.

As mentioned in section 2, high latency and significant signal degradation are significant issues in securely transmitting data from node to node. Specific strategies to mitigate this are discussed in section 3. But when it comes to the design of the connections themselves, it's important to consider  frequencies used during transmission, or the duplex of such connections. In general, each node send data, and receive data via their physical layers, via their transducers.

![[Pasted image 20250221200625.webp|701]]
$$\text{Fig 2. Network Layer for diagram}$$

Most networks use half-duplex (TDD) due synchronisation issues and costs of full duplex but can use frequency duplexing by splitting by uplink and down link communication or time duplexing by nodes alternating sending and receiving in short bursts[7].
This allows more efficient and faster communication, simply by being more responsive. This can be further helped with the frequency used during the communication. Despite Channel data capacity scaling with range of frequency, the attenuation (or multi-path fading) also increases with higher frequencies, which increases the error rate [ 6 ] /[13] . In response to this, different ranges of frequencies are used for different lengths of communication, with shorter ranges, allowing higher frequencies.

| Frequency Range (Hz) | Typical Application         | Depth/Range                | Approximate Data Rate  | Comments/Trade-offs                                                                                                                                                                                     |
| -------------------- | --------------------------- | -------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 100 – 1,000          | Long-range communication    | Deep water (>1 km)         | ~1–5 Kbps              | Lower attenuation supports long-range propagation; limited bandwidth results in lower data rates. Robust modulation (e.g., FSK, BPSK) is preferred.  [13]                                               |
| 10,000 – 50,000      | Moderate-range applications | Medium depth (up to 500 m) | ~10–50 Kbps            | Offers a balance between range and data rate; modulation techniques like QPSK or OFDM help manage attenuation and multipath effects. [17]                                                               |
| 50,000 – 100,000     | Short-range, high data rate | Shallow water (<500 m)     | Up to 100 Kbps or more | Higher frequencies provide increased bandwidth and data rates, yet suffer from more significant attenuation and require higher order modulations (e.g., 16-QAM, 64-QAM) with complex equalization. [16] |



Lower frequencies prefer long-range connections at the cost of bit, while higher frequencies have higher throughput for shorter distances but at cost of significant degradation. In many modern systems, adaptive modulation techniques are also used, allowing the system to dynamically adjust the modulation scheme based on current channel conditions, thereby optimizing throughput and minimizing error rates [16]



**3.1 Algorithms and protocols to maintain throughput**

Many protocols and algorithms used in UWN overlap with traditional networks such as TCP/IP although there are significant differences. Both systems allow for retransmissions of erroneous packets [6] via send ACK's or Acknowledgements or implementing a time out system, where if responses don't occur in a "reasonable" time. The time out length in UWA systems however are significantly longer in comparison, and algorithms such as "fast retransmission" [8] where a packet is retransmitted if the sender receives 3 duplicate ACK's. UWN wouldn't be fast enough to make good use of this and sending duplicate packets in general is very power inefficient.

Error and corruption of packets due to interference and multipath propagation must also be considered during the design, through such strategies such as Forward error correction (FEC) methods Methods and adaptive modulation and coding(AMC) [13].
Both protocols are relatively simple, whether it be ensuring a receiver or relay, correct any errors found with packets before handling them further or adjusting transmission parameters such as rates and frequency used based on channel conditions. These dynamic real-time adjustments, help minimise likelihood of failure and therefore, necessity of retransmission, heavily increasing throughput.


**4 Measuring Bit rate and Power Usage of UWN in a multi hop network**

In sections 2 and 3, I have mentioned the key factors effecting performance in UWN whether that be power usage, interference, low bit rate, topology used and much more. Through an example, I want to explore bit rate and power usage expected and how it is measured and affected in UWN. It will use JANUS , the Underwater Communications Standard a modern, interoperable standard for underwater acoustic modems. [14]

Typically for JANUS devices, an effective frequency of 6kHz and we can assume an average distance of 1KM between nodes and standard shallow water conditions.

Typically, Shannon’s capacity theorem gives us  theoretical maximum channel capacity [12] :
$$C = B \log_2(1 +SNR)$$
Where "B" refers to bandwidth and "SNR" refers to signal to noise ratio of the connection, measured in dB. With an example SNR of 10db, we can get a total theoretical capacity of 20,760bps, or 20 kbps. In practice, when handling error correction, redundancy and synchronisation of sending messages to minimise interference, it is typically within 80-200bps.
	
As mentioned in section 2, with the use of the UNESCO [4] equation which uses temperature, salinity and pressure, to get (in typical conditions) a speed of 1507m/s of sound travelling through sea water, for a typical hop distance 1000m, hop time(H(t)) would be 0.66 seconds.

Power consumption in underwater channels increases with distance due to the exponential nature of acoustic attenuation. This is modelled as:$$A(d)=d^k×[a(f)]^d$$
Where d is distance, k is spreading factor (2 for spherical spreading) and a(f) is the frequency‐dependent absorption factor, essentially the damping of sound per km, hence requiring more energy to produce a stronger signal over long distances. [15]

For 6Khz, an absorption rate of 1.12 is expected for sea water or, every km, power is multiplied by 1/1.12. So 89% signals strength per km. So when applied back to find how attenuation effects, distance and spreading power consumption, we get:

$$A(2) = 2^2 \times 1.12^2 \approx 4 \times 1.254 \approx 5.018$$
This tells us that for a 1 km hop in comparison to a completely lossless channel, a transducer in a UWN it would require 5x more power for a 1 km hop.

This poor performance is a strong demonstration of both the challenges left with underwater communication but also the necessity to minimise power usage, via error correction, multi-hop topology with relays and efficient power replacement. This can include self-powering techniques such as solar panels or even using AVN's to replace battery packs.[6]

**Conclusion:**

This literature review has explored the performance of underwater acoustic networks by highlighting both the necessity of these systems in marine research and the physical challenges posed by the underwater environment. We have examined key issues such as multipath propagation, fading, high latency, bandwidth limitations, power constraints, and the difficulties of maintenance and repair. Although many current implementations rely on centralized architectures with surface buoys, or sensors that simply are extracted to the surface [9] ongoing projects—such as the Subsea Internet of Things [10]  and TARF—aim to replicate the flexibility of terrestrial networks by enabling underwater nodes to operate more independently [11] .



##### References
----

[1] Fava, M. (2022). _How much of the ocean has been explored?_ Retrieved from [https://oceanliteracy.unesco.org/ocean-exploration/](https://oceanliteracy.unesco.org/ocean-exploration/)
[2] Akyildiz, I. F., Pompili, D., & Melodia, T. (2005). Underwater acoustic sensor networks: Research challenges. _Ad Hoc Networks, 3_(3), 257–279. [https://doi.org/10.1016/j.adhoc.2005.01.004](https://doi.org/10.1016/j.adhoc.2005.01.004)

[3] Qu, Z., & Lai, M. (2024). A review on electromagnetic, acoustic, and new emerging technologies for submarine communication. _IEEE Access, 12_, 12110–12125. [https://doi.org/10.1109/ACCESS.2024.3353623](https://doi.org/10.1109/ACCESS.2024.3353623)

[4] Greenspan, M., & Tschiegg, C. E. (1957). _Speed of sound in seawater at high pressures._ Retrieved from [https://nvlpubs.nist.gov/nistpubs/jres/59/jresv59n4p249_A1b.pdf](https://nvlpubs.nist.gov/nistpubs/jres/59/jresv59n4p249_A1b.pdf)

[5] Zahedi, Y. K., Ghafghazi, H., Ariffin, S. H. S., & Kassim, N. M. (2011). Feasibility of electromagnetic communication in underwater wireless sensor networks. In _Proceedings of ICIEIS 2011, Part II._ [https://link.springer.com/chapter/10.1007/978-3-642-25462-8_55](https://link.springer.com/chapter/10.1007/978-3-642-25462-8_55)

[6] Proakis, J. G., Sozer, E. M., Rice, J. A., & Stojanovic, M. (2001). Shallow water acoustic networks. _IEEE Communications Magazine, 39_(11), 114–119. https://doi.org/10.1109/35.965368

[7] Sozer, E. M., Stojanovic, M., & Proakis, J. G. (2000). Underwater acoustic networks. _IEEE Journal of Oceanic Engineering, 25_(1), 72–83. https://doi.org/10.1109/48.820738

[8] Eddy, W. (Ed.). (2022). _Transmission control protocol (TCP)_ (RFC 9293). Retrieved from [https://datatracker.ietf.org/doc/html/rfc9293](https://datatracker.ietf.org/doc/html/rfc9293)

[9] Mohsan, S. A. H., Yanlong, L., Sadiq, M., Liang, J., & Khan, M. (2023). Recent advances, future trends, applications and challenges of Internet of Underwater Things (IoUT): A comprehensive review. _Journal of Marine Science and Engineering._ [https://doi.org/10.3390/jmse11010124](https://doi.org/10.3390/jmse11010124)

[10] Konowe, C. (2023). Marine telemetry: Shedding light below the waves [Article]. Retrieved from [https://www.marinetechnologynews.com/news/marine-telemetry-shedding-light-628841](https://www.marinetechnologynews.com/news/marine-telemetry-shedding-light-628841)

[11] Tonolini, F., & Adib, F. (2018). Networking across boundaries: Enabling wireless communication through the water-air interface. https://doi.org/10.1145/3230543.3230580

[12] A Mathematical Theory of Communication

[13] - Stojanovic, M., & Preisig, J. (2009). Underwater acoustic communication channels: Propagation models and statistical characterization. _IEEE Communications Magazine_.

[14] - JANUS

[15] - - Urick, R. J. (1983). _Principles of Underwater Sound._

[16]  On the relationship between capacity and distance in an underwater acoustic communication channel

[17]  The state of the art in underwater acoustic telemetry