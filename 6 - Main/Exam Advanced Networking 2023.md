2025-01-15 12:21

Status:

Tags:[[Advanced Networking]]

---
**Question 1:**

**The TCP/IP protocol has evolved considerably since its initial specification nearly forty years ago. Several extensions were introduced to deal with the problems associated with networks with a high bandwidth-delay product, also known as “long fat networks”, and there have been a range of solutions proposed to deal with the shortage of IPv4 addresses.**

- **a) Describe the problems which are caused by a high bandwidth-delay product. Which features in the TCP standard as originally designed make such networks problematic for high-performance networking?** 
  **Assuming the speed of light is `3*10^8` metres per second, calculate the maximum rate at which data can be sent between two computers 3000 kilometres apart using unextended TCP. [8 MARKS]**
  
  a
  
- **b) Consider an application which has been written to use UDP for single-shot “query” and “response” operations. Considering the same 3000km separation, how long will each such operation take? State any assumptions that you make.**
  **If an application needs to reliably perform five hundred (500) such operations per second, what approaches might be used to allow this to work? [8 MARKS]**
  
  1 packet would take `0.01` seconds to get to other end, so `20ms` round trip. Meaning if it did 1 full cycle before sending the next packet, it could only get `50` queries resolved. 
  Using a Pipeline approach however and sending multiple packets in parallel even before receiving a response from the previous ones, you could potentially have 500 operations done in 20ms. Although not to overall 
  
- **c) There is a global shortage of IP version 4 addresses. Explain briefly the causes of this, and suggest two possible ways to expand the number of addresses available for allocation. [4 MARKS]**
  
  Only `2^32` so 4 billion unique addresses. Initially 32 bits was seen as over kill for how small the internet was at the time and projected to be. The main solution is Ip v6 which is 128 bits and has `2^64` available address spaces. Another solution is just better allocating the range of 

**Question 2:**

**TCP is the dominant transport protocol used on today’s Internet.**

- **(a) TCP uses the mechanism of a “sliding window” to manage reliable transmission and reception of data. The window defines the amount of unacknowledged data that is in flight.**
  **Explain the operation of the sliding window, with reference to the operation of both the sender and the receiver’s window. Your answer should include a description of how the sender processes data which applications pass down for transmission, and how the receiver processes arriving packets prior to passing data to an application. [10 MARKS]**
  
  
  

- **(b) The operation of TCP relies heavily on the timely and efficient sending of acknowledgements to indicate the successful arrival of data.** 
  **Explain the operation of TCP’s acknowledgement mechanism. What data is acknowledged, and when are those acknowledgements sent? When choosing an acknowledgement strategy, what are the implications for performance in terms both of efficiency and latency? Your answer should compare and contrast two alternative strategies. [10 MARKS]**
  
  An acknowledgment or an ACK is confirmation  
  





##### References
----
[Exam 2023](file:///C:/Users/Asus/Documents/School/Final_Year/Advanced_Networking/Exam_Papers/LHM%20Advanced%20Networking%202022-23.pdf)