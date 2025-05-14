2024-12-21 13:36

Status:

Tags: [[Pragmatic Programmer]]

---
Tips from the pragmatic programmer on how to debug in order of how it should be done.

1. READ THE DAMN ERROR MESSAGE
   
2. Take a moment to understand what the actual piece of code is meant to do
   Break in down into an algorithm and what the dependencies and processes of that algorithm are. Is it doing what is required
   
3. Binary search the bug down:
   What I mean by that is split the dependent code by half and see if those values are correct. If they are, look at half way down. If values are wrong there, look halfway up.
   
   Doing this for a code space of e.g. 64 frames, it would take up to 6 times to find the faulty frame. You can make this more efficient by looking at the most crucial or most likely to fail sections.
   
4. Replicate the issue and solution elsewhere in a smaller script.
   
5. Use VScode debugger to track the value of data across code

## General Advice

- Assume your code/input is wrong, not the library
- At every point of being overwhelmed, step back and think what you're trying to do, why and what is needed for that purpose.
- Assume edge cases will happen constantly so handle them as soon as you can.

##### References


----
[The Pragmatic Programmer](file:///C:/Users/Asus/Downloads/The%20Pragmatic%20Programmer%20Your%20Journey%20to%20Mastery,%2020th%20Anniversary%20Edition%20by%20Andrew%20Hunt%20David%20Hurst%20Thomas.pdf)