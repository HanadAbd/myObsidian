2025-01-23 10:04

Status:

Tags: [[Dependable and Distributed Systems]]

---
Lecture 2 on Week 1
Lecture 3 on Week 2

### *Note:*
*Brief introduction topic to the module so not **too** important to make flash cards about beyond the definitions of the taxonomy*

**Key Points from lecture:**
- **Exam questions are split 40,30,30 in terms of marks.** 
- **First question relates to topic 2,3,4 and is related to core dependability from the first 1/3rd of the module** 
- **He mentioned having a strong understanding of the taxonomy terms would be useful**

**TOPICS:**
- Dependability Impairments  
- Dependability Means  
- Dependability Attributes

### Dependability

Dependable is when a system is **trust worthy** enough to be **justifiably** placed on the **service** it provides. This is incredibly relative since some systems might not need to be as reliable (e.g. Planes should be more reliable then a laptop). So we would need a measurement for dependability and justification against system.  

**Service** or **services** are the behaviours the users sees via an interface. To be trustworthy, they need to be **timely** and **correct** (based on context, e.g. some real time data might be discarded if arrived before a deadline, or still could be useful.)

Components needed to develop a dependable system are:

**System Models**: Description of how we view/think of our system. So in terms of layers of abstractions, white boxes, black boxes, dependency of components etc. 
They are comprised of a set of **elements** with well defined interfaces to provide a service.
An **element** being component that provides a pre-defined service whilst working with
**PLEASE FLESH OUT THIS DEFINITION**

**Fault Models**: Description of **fault** problems that can occur in a system. Typically caused by poor assumptions of the importance of issues, hardware problems , complexity and dependency of "**black boxes**" so libraries and hardware that can go wrong but we wouldn't be able to view.

**Specification (Very General Definition)**: Defines how a system **should** work and behave. Has 2 fundamental principles regarding 1. Safety (so response and minimising failure) and 2. Liveliness (contribution to the useful functionality of the system, the good)

### Taxonomy of Dependability

![[Pasted image 20250123101133.webp]]

The dependability trees fundamental principals of what it means for a system to be dependable. Not all factors as important as others, but this as far as those key ideas can be decomposed while still being fundamental and useful.
So dependability could be seen as a composite measurement of these key ideas.

### Impairments 

Factors that endanger the dependability of a system

**Failure**: An Observable deviation from specification (not necessarily observable to a human, it could be a system check, compiler, parser error etc.)

**Error**: Unexpected and incorrect change in state that can lead to failure, but not necessarily. Not necessarily detectable either.

**Fault**: Lowest level and more hypothetical. Any "reasonable" event that can cause an error. Hardware faults are broken down into permeant (active fault unless stopped), transient (temporarily active) and intermittent (active periodically) with transient being the most common.

So pipeline Fault-Error-Failure Cycle or **Fundamental Chain**: is fault -> error -> failure
![[Pasted image 20250123140515.webp]]

Failure in 1 layer abstraction could be a fault to next layer, essentially propagating faults across all layers
### Means

What we can do to add dependability attributes into our system in the presence of **impairments**. Refers to how to handle faults that can occur in a system

- **Fault Prevention**: hinder and obstruct cause and spread of faults
- **Fault Removal**: reducing, reducing likelihood and consequences of faults typically with **validation** of set defined properties, **diagnosis** of problems and **corrections** modifying the systems to allow properties to be met
- **Fault forecasting**: estimating the number ,likelihood and wider consequences of faults in system. To aid with, can use fault injection, so purposefully introducing faults to see system response and if it causes failure
- **Fault tolerance**: Since faults are inevitable, and there will always be a fault model, what faults and errors you' re willing to tolerates depends on the system, and some level of tolerance will always exist. 

### Attributes (Dependability Attributes)

Metrics or measurements for dependability of a system, in relation to system purpose (depending on the system, safety and availability might be more important then other factors, in another system it could be the other way around.)

---

**Reliability**: Probability of system delivering correct services over a specified time period. (Depends on the context of the system how high a reliability is needed e.g. more reliability for plane in air then sky). Commonly confused with availability.
Reliability regimes:
- **Fail-safe Systems**: When there's a failure, applications safely halts and makes alerts and changes as needed. So safe when they do not operate
- **Fail-operational Systems**: Continues to operate when they fail,
- **Fail-Secure Systems**: maintains maximum security when they can not operate. Most challenging to implement since you won't know what context it's occurring e.g. locking doors in fire
- **Fail-silent Systems**: when an internal failure is detected, functions correctly or stops after. Dying cleanly and not informing anything else
- **Fault-tolerant Systems**: Continues to operate correct when subsystems operate incorrectly

**Availability**: function of time where the probability of a service provided by a system is operating correctly and able to perform it's function. Typically used with MTTF (meant time to failure) and MTTR (mean time to repair), in order to get downtime per year

**Safety**:  extent to which a system can operate without damaging it's environment. Some system have "safe" statuses, that can go to when there's a known issue or failure

**Confidentiality**: non-disclosure of undue information to unauthorised entities. 

**Integrity**: Absence of improper system alterations, and should be available to change by those with valid access

**Maintainability**: time representing the probability that a failed computer system will be repaired in t time.
### Security

Combined with Availability, and Integrity, make CIA which is referred to as the security triad so security is a part dependability

### Software Fault Tolerance

*Before it could be both software and hardware, but this is more software

Software is increasingly defining the functions of most systems, with complexity increasing and fault free code being harder to develop.

If a program for a given fault model can only satisfy safety, it is said to be **fail-safe f-tolerant** and if only liveness, then **non-masking f-tolerant**. If neither, the **f-intolerant**. if both, then **masking f-tolerant**

Allows to make a partial order of fault Tolerance Classes, for the importance:

![[Pasted image 20250123150008.webp]]

What's needed for fault tolerance

Using 2 program components, detectors and correctors

Detectors assert the validity of a predicate in a running program. Necessary and sufficient to design fail-safe fault tolerance

corrector that imposes a given predicate on a running a program e.g. exception handlers Necessary and sufficient to design non- masking fault tolerance

both make for masking fault-tolerance

### Connection between fault tolerance and impairment

**TODO: COMPLETE THIS SECTION past the 59th minute of the topic video**

Phases of fault tolerance, transition diagram between the different states a system can be in

![[Pasted image 20250123151345.webp]]


##### Glossary
---

##### References
----
[02 Dependability Concepts](file:///C:/Users/Asus/Documents/School/Final_Year/Dependable_and_Distributed_Systems/Topic_2_Dependabilitiy_Concepts/02%20Dependability%20Concepts.pdf)
![[02 Dependability Concepts.pdf]]