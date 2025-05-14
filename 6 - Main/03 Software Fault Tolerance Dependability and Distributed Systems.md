2025-01-30 09:58

Status:

Tags: [[Dependable and Distributed Systems]]

---

Lecture 4 on Week 2
Lecture 5 on Week 3

*Key notes:*
- Well researched and structured is the most important for the coursework
- After Week 3, should be able to answer all that is necessary for Question 1, so topics 2,3,4
- NVP, Recovery blocks and modelling are very important

**Topics**:
- Detectors and Correctors  
- Checkpointing  (Not Too important but good to at least know how **recovery lines** work)
- Recovery Blocks (Very Important)
- N-Version Programming (Very Important)  
- Fault Injection Analysis  
- Parameter Estimation

### Software Systems Fault tolerance

If a system, can still satisfy a specification, even after a fault model is applied to it, it is referred to as **F-Tolerant**.

You can use formal methods for a system specification with
- **Safety**, which suggest something bad happens over a finite time (steps, duration etc. just a fixed window of time)
- **Liveness**, which suggests something good will **eventually** happen, regardless of how long


2 fundamental components, for ensuring safeness and liveness as detectors and correctors, to asset correctness and response to that. 

![[Pasted image 20250208140601.webp]]
This can be be implemented into the fault error cycle such as:

![[Pasted image 20250208140753.webp|785]]

Where error detection is done by detectors, and error recovery by correctors. Faults can't be detected but errors are since they are always observable.

Some example of detectors:
- Parity checks
- Validity of calculations (dividing by 0 or buffer overflow)

With corrector example being:
- Exception Handlers

### States of a software System

Once we reach an erroneous or failure state of a system, we can respond in 2 main ways,

**Forward Error Recovery**: Upon error, program moves to state which is no longer erroneous
**Backwards Error Recovery**: Upon error, goes back to previous recorded non - error state (e.g. checkpoints in distributed databases to rollback to for transactions.)

### Difficulty with checkpoints and need for Recovery Line for Backwards Error Recovery

It's hard to find universally agreeable previous state that all distributed databases can agree on, to maximise consistency. 1 previous state might work for A, but not B so A would need to go further back, making checkpointing more out of date.

**Recovery lines** are useful since they are essentially just guidelines for **when** to do a checkpoint, Typically being done when a system has no change to state. E.g. When no message is going to be received, so every send needs a recieved

### Recovery Blocks

*IMPORANT TOPIC: Should be able to draw*
Recovery blocks is a technique for ensuring safety ness and liveness by essentially having multiple back up components that can handle a task to the standard of acceptance test, so N backup solutions.

So 1 hardware channel, with n software channels. With the software channels being slighty different solutions for the same goal.

The acceptance test goal is the hardest part (and main section )and what it should include depends on context but typically:
- Error in module operation
- Time limitation of solution
- Raised expectation

We restore the system state until we run out of secondaries or pass.

![[Pasted image 20250208141740.webp]]
So by definition, redundant and time consuming, but really helpful in tolerating flaws and errors.

### N- Version Programming:

N independent functionally equivalent programs, characterised as N hardware channels and N software channels.

Used to view discrepancy of results where their shouldn't be and indicates an issue, since they should match.

Typically used with **majority voting** where 3 channels to get the majority value, but even N=2 could inform us of a discrepancy. 

Could preserve liveness by using the most likely to be accurate value , or even having each machine go back to a safe space (e.g. the start space ) 


A driver will invoke each version for a **round of voting** although since they aren't guarantee to take the same time, synchronisation will be necessary. Accuracy is also a big issue amongst version, whether that be issues with consistent floating point accuracy or some other hard to maintain value or other issues that don't even have to do with the N versions (e.g. different languages, different hardware etc.)

NVP axiom is: NVP is most accurate when each version failure is completely independent to each other, so failing in different ways and they don't all fail on the same input  


### Fault Injection
*Not too important*
Actively inserting known faults into a system in order to see how it handles it e.g. Really fucked up user input.

Can be implemented early in the development cycle, even during prototyping but works best when the system is complete and operational, to see how it handles it in context.

In order to not affect liveness, they can use **coverage** or just the ration of number of test passed, against how many is required.
![[Pasted image 20250208145239.webp]]





##### Glossary
---

##### References
----
[03 Software Fault Tolerance](file:///C:/Users/Asus/Documents/School/Final_Year/Dependable_and_Distributed_Systems/Topic_3_Fault_Tolerance/03%20Software%20Fault%20Tolerance.pdf)

![[03 Software Fault Tolerance 1.pdf]]