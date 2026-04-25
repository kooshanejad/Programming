# Graphs (Week 11)

## Task 1
Dijkstra's algorithm is used to find the shortest path in a weighted graph, but it only works correctly when all edge weights are non-negative. This is because once Dijkstra's algorithm chooses the current shortest distance to a vertex, it assumes that distance is final. Negative weights can break this assumption. For example, consider this graph:
```
A --2--> B
A --5--> C
C --(-4)--> B
```
Since 2 is smaller than the distance from A to C, which is 5, it treats B as already having the shortest path. However, there is actually a shorter path:

```
A -> C -> B
5 + (-4) = 1
```
So the true shortest distance from A to B is 1, not 2. Dijkstra's algorithm can fail because the negative edge from C to B creates a shorter path after B has already been processed. Because of this, Dijkstra's algorithm should not be used when a graph contains negative edge weights.
