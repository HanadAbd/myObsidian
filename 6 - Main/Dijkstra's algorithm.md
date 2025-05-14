2024-12-16 11:15

Status:

Tags:

---
A simple path finding algorithm that assigns a value to each node. Each node having a cost of INF and a parent node.

We have a list with just the start node, and expand it to get the neighbours. We then constantly keep expanding the shortest node until we've expanded the final node.
![[Pasted image 20241216113707.webp|588]]

As an example in this case, start node is D and want to get the shortest point from there so. List begins with just D. That we expand and remove to get A and E, with their associated costs e.g. D+E which is 2+0 = 2. We expand E since it's the smallest and now our list of nodes includes:  A,C,G.
With everything we expand, we pass the parent node of what's being expanded to the children node.
So since A = D+A which 0+4 = 4, we expand that since C = D+E+C = 0+2+4 == 6. We then continuously do this until every node is expanded.

This has a time complexity of O(v^2) where v is every verticy.




##### References


----
[w3Schools](https://www.w3schools.com/dsa/dsa_algo_graphs_dijkstra.php)