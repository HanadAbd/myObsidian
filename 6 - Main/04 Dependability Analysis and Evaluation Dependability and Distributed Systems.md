2025-02-08 14:42

Status:

Tags: [[Dependable and Distributed Systems]]

---

Key Note:

- Most important topic for the first question. 
- Should be able to model TMR system for any reliability modelling diagram
- Should be able to create condensed state model, and showing states and from state probability modelling

Summary: 

More so for implementation of dependability early in design instead of after thought

***Topics***:

- *Hazards, Risks and Safety*
- *Exponential Failure Law*  
- *MTTF, MTTR and MTBF*  
- *Combinatorial Modelling*  
- *Cut Set and Tie Sets*  
- *Markov Models*
### Safety requirements and Hazards

Safety critical systems have safety requirements that the system will have to comply with by identifying hazards.
Hazards being a state or set of conditions that will lead to an accident, usually defined in terms of state to be avoided.

Measured in severity and frequency in order to rank them priority, so we support the most important hazard the most.
Which time scale is important and measure of severity if very context dependent.

Risk is hazard level, but also likelihood of hazard, and exposure.

Safety cases, are a clear argument that a system is acceptably safe to operate in a particular context. These are required to certify the use of high critical systems,

- Preliminary safety cases
- Interim safety case
- Operation safety case

### Hazard Analysis

 Hazard analysis is a structured reasoning of a system in harm it can cause, includes techniques:
 
 - **FMEA (Failure Modes and effects analysis):** Consequence of single failures and the hazards and hazardous situations that come from it.
 - **FMECA (Failure Modes, Effects and Criticality Analysis )**:  Similar to FMEA but more based on high priority realistic failures instead of every failure. More cost and time effective. 
 - **HAZOP (Hazard and Operability study)**:  Focuses on handling on "What if?" questions to test the handling of many situations to see what risks there are. Only really useful with an expert of the system that can answer these questions
 - **Event trees**: Starting from event that can effect the system, track forward to determine the effects of both normal and fault events
 - **Fault trees**: Similar to event trees but working back from hazardous situations to view possible causes, so simpler and more concise then event trees.

### Exponential failure law

The exponential failure law tells us the likelihood of how long a device will continue without failure. It tells us that by nature, reliability reduces over time


The diagram shows the average lifetime of a system, divided into it's *infancy*, *useful life* and *worn out* stages. 
Failure rate is the expected number of failures of a certain device over a given time frame represented as $\Lambda$ In our case we're assuming that **fault rate is constant**. So fault rate during it's useful life.

![[Pasted image 20250208163548.webp]]

Most faults in infancy and worn out stages.

### Mathematical Modelling of reliability, hazardousness and availability

For *N* devices starting at t0, U(t) nodes are up and F(t) are down.

**Reliability**  = **R(t)** => $\frac{U(t)}{U(t) + F(t)} = \frac{U(t)}{N} = 1 - Q(t)$

**Unreliability**  = **Q(t)** => $\frac{F(t)}{U(t)+F(t)} = \frac{F(t)}{N} = 1 - R(t)$

**Hazard rate/failure rate** = **z(t)** => $\frac{1}{U(t)}\frac{dF(t)}{dt}$
Tells us the likelihood that will a system will fail fail at time $t$ given it has survived up to $t_0$

**Exponential Failure Law** = **R(T)** => $e^{-\lambda t}$
So if failure rate was 0.01 fails/hour, at t= 50 hours, chance of working is 61%

**MTTF (Mean time to Failure)** => $\frac {1}{\lambda}$
MTTF being the expected time a system will operate without issue

**MTTR (Mean time to repair)** => $\frac{1}{\mu}$
Average time to repair a failed system, where $\mu$ is rate of repair

**Availability** => $\frac{MTTF}{MTTF+MTTR} => \frac{100}{100+5} => \text{ available 95.2\%  of the time}$
How often the device is available

$\text{MTBF = MTTR +MTTF}$
Mean time between failures

### Assumptions during mathematical modelling

There are some base assumptions for all of our mathematical modelling to make it simpler

- Always constant failure rate, so $\Lambda$ is constant.
- Failures are independent of each other, not increasing the chances of future failures.
- Always fully functional after repairs.
### Reliability Modelling/Combinatorial Models

Combinatorial models are models of a system we can use calculate reliability, an example being relaiblity block diagrams.

![[Pasted image 20250210113812.webp]]

Comprised of:
- **Series Systems:** All components have to work together to operate correctly.
	P(success) = P(all work)
- **Parallel System**: Only 1 component has to work to operate correctly.
	P(success) = 1 - P(all fail)
- **M of N Parallel System**: Only M of N systems have to work in order to operate correctly. The most complex of the 3 and technically a combination of parallel and series system  

Using this, we can get an upper bound and lower bound of reliability with cut sets and tie sets

- **Cut Sets**: Lower bound of reliability by finding the minimal sets of sequences when failures would lead to **system failure**.
	C=1 for series. C = N for parallel.
- **Tie Sets**: Upper bound of reliability. Same as cut sets but minimal sets of sequences for a **correctly working system**.
	C=N for series. C=1 for parallel.

### Reliability Modelling example

Using **Triple Mode redundancy (TMR)** which has 3 processors in parallel, who's output is compared for inconsistency, and uses majority voting, so 2 of 3 must agree for valid output.

![[Pasted image 20250210114906.webp]]


### Markov Modelling

We're using continuous time Markov chains, which have a discreate state space and continuous time state.

Comprised of:
- State: 
- State Transition: How sat


##### Glossary
---

##### References
----
04 Dependability Analysis and Evaluation

![[04 Dependability Analysis and Evaluation.pdf]]