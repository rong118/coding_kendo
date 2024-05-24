# Minimum Spanning Tree

A Minimum Spanning Tree (MST) of a weighted, undirected graph is a spanning tree whose total edge weight is the minimum possible among all spanning trees of the graph.

## Key Concepts:

- **Graph**:

A collection of vertices (or nodes) connected by edges. In a weighted graph, each edge has an associated numerical value (weight).

- **Spanning Tree**:

A subgraph that includes all the vertices of the original graph, is connected and contains no cycles. Essentially, it "spans" all the vertices with the minimum number of edges.

- **Minimum Spanning Tree**:

Among all possible spanning trees of a graph, the MST is the one with the smallest possible sum of edge weights.

## Find an MST:

There are several well-known algorithms for finding an MST in a graph:

- Kruskal's Algorithm
  
- Prim's Algorithm

## Kruskal's Algorithm:

Sort all the edges in the graph by increasing weight.
Add edges to the MST, in order of their weight, as long as they don't form a cycle with the already included edges.
Stop when the MST contains V−1 edges.

## Prim's Algorithm:

Start with an arbitrary vertex and grow the MST one edge at a time.
At each step, add the smallest edge that connects a vertex in the MST to a vertex outside the MST.
Repeat until all vertices are included in the MST.
