2025-01-09 15:22

Status:

Tags:

---

We have 2 buffers/arrays:
- Frame buffer with all the coordinates for all the vertices at every point
- Z-Buffer which has the distance for each point of the screen, intially set as 0 to say it's infinitely far away. Helps to differentiate between points close to and those far away, to get a 2d projection of the rendering.



##### References


----
