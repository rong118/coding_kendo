# Minimum Spanning Tree

A Minimum Spanning Tree (MST) of a weighted, undirected graph is a spanning tree whose total edge weight is the minimum possible among all spanning trees of the graph.

## Key Concepts:

- **Graph**:

  A collection of vertices (or nodes) connected by edges. In the weighted graph, each edge has an associated numerical value (weight).

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

### Workflow of Kruskal's Algorithm:
- Initialization:

  Create a list of all edges in the graph, sorted by their weight. Initialize a data structure (typically a Disjoint Set Union/Find structure) to keep track of which vertices are in which components.

- Algorithm Execution:

  Iterate through the sorted edges, adding the smallest edge to the MST if it doesn't form a cycle with the already included edges. This is determined using the Union-Find data structure. Continue this process until the MST contains V−1 edges, where V is the number of vertices in the graph.

- Result:

  The edges added during the iteration that form the MST

### C++ Implementation
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Edge {
public:
    int src, dest, weight;
    Edge(int s, int d, int w) : src(s), dest(d), weight(w) {}
};

// Comparator to sort edges by weight
bool compareEdges(Edge a, Edge b) {
    return a.weight < b.weight;
}

class DisjointSet {
    vector<int> parent, rank;
public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
        }
    }

    int find(int u) {
        if (parent[u] != u) {
            parent[u] = find(parent[u]); // Path compression
        }
        return parent[u];
    }

    void unionSets(int u, int v) {
        int rootU = find(u);
        int rootV = find(v);
        if (rootU != rootV) {
            if (rank[rootU] < rank[rootV]) {
                parent[rootU] = rootV;
            } else if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++;
            }
        }
    }
};

vector<Edge> kruskalMST(vector<Edge>& edges, int V) {
    vector<Edge> mst;
    DisjointSet ds(V);
    
    // Sort edges by weight
    sort(edges.begin(), edges.end(), compareEdges);

    for (Edge& edge : edges) {
        int u = edge.src;
        int v = edge.dest;
        int weight = edge.weight;

        // Check if the current edge forms a cycle
        if (ds.find(u) != ds.find(v)) {
            mst.push_back(edge);
            ds.unionSets(u, v);
        }
    }

    return mst;
}

int main() {
    int V = 4; // Number of vertices
    vector<Edge> edges;
    edges.push_back(Edge(0, 1, 1));
    edges.push_back(Edge(0, 2, 3));
    edges.push_back(Edge(1, 2, 3));
    edges.push_back(Edge(1, 3, 6));
    edges.push_back(Edge(2, 3, 4));

    vector<Edge> mst = kruskalMST(edges, V);

    cout << "Edges in the Minimum Spanning Tree:" << endl;
    for (Edge& edge : mst) {
        cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
    }

    return 0;
}
```

## Prim's Algorithm:

Start with an arbitrary vertex and grow the MST one edge at a time.
At each step, add the smallest edge that connects a vertex in the MST to a vertex outside the MST.
Repeat until all vertices are included in the MST.

### Workflow of Prim's Algorithm:
- Initialization:
  - Start with a single vertex (arbitrary choice).
  - Maintain a list of edges that connect vertices inside the MST to those outside.
  - Use a priority queue (min-heap) to efficiently get the smallest edge connecting the MST to the rest of the graph.

- Algorithm Execution:
  - Initialize all vertices as not being part of the MST.
  - Select the initial vertex and mark it as part of the MST.
  - Add all edges from this vertex to the priority queue.
  - While there are vertices not in the MST:
    - Extract the smallest edge from the priority queue.
    - If the destination vertex of this edge is not yet in the MST:
      - Add this edge to the MST.
      - Mark the destination vertex as part of the MST.
      - Add all edges from this new vertex to the priority queue.

- Result:

  The edges added during the iteration form the MST

### C++ Implementation
```c++
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <functional>

using namespace std;

typedef pair<int, int> Edge; // first: weight, second: destination vertex

vector<Edge> primMST(vector<vector<Edge>>& graph, int V) {
    vector<Edge> mst;  // Resulting MST edges
    vector<bool> inMST(V, false);  // Track vertices included in MST
    priority_queue<Edge, vector<Edge>, greater<Edge>> pq;  // Min-heap priority queue
    
    // Start with the first vertex (0)
    inMST[0] = true;
    for (auto& edge : graph[0]) {
        pq.push(edge);
    }

    while (!pq.empty()) {
        Edge edge = pq.top();
        pq.pop();
        int weight = edge.first;
        int v = edge.second;
        
        if (inMST[v]) continue;
        
        inMST[v] = true;
        mst.push_back(edge);

        for (auto& nextEdge : graph[v]) {
            if (!inMST[nextEdge.second]) {
                pq.push(nextEdge);
            }
        }
    }

    return mst;
}

int main() {
    int V = 4; // Number of vertices
    vector<vector<Edge>> graph(V);

    // Add edges to the graph
    graph[0].push_back({1, 1});
    graph[0].push_back({3, 2});
    graph[1].push_back({1, 0});
    graph[1].push_back({3, 2});
    graph[1].push_back({6, 3});
    graph[2].push_back({3, 0});
    graph[2].push_back({3, 1});
    graph[2].push_back({4, 3});
    graph[3].push_back({6, 1});
    graph[3].push_back({4, 2});

    vector<Edge> mst = primMST(graph, V);

    cout << "Edges in the Minimum Spanning Tree:" << endl;
    for (Edge& edge : mst) {
        cout << edge.second << " with weight " << edge.first << endl;
    }

    return 0;
}
```

## Prim's Algorithm VS. Kruskal's Algorithm

Prim's algorithm and Kruskal's algorithm are both greedy algorithms used to solve the Minimum Spanning Tree (MST) problem, but they differ in their approach:

- **Choice of starting vertex**
  - Prim's algorithm starts with an arbitrary vertex and grows the MST from that vertex.
  - Kruskal's algorithm does not require a specific starting vertex; it processes all edges in the graph.

- **Edge selection**
  - Prim's algorithm selects the edge with the minimum weight that connects to the current node (i.e., the edge with the smallest weight that has one endpoint in the MST and the other endpoint outside the MST).
  - Kruskal's algorithm selects the edge with the minimum weight from all edges in the graph.

- **Union operation**
  - Prim's algorithm performs a union operation on the nodes connected by the selected edge, effectively merging two sets into one.
  - Kruskal's algorithm also performs a union operation, but it does so for each connected component (i.e., each set of nodes that is not yet part of the MST).

- **Time complexity**
  - Prim's algorithm has a time complexity of **O(E + V)**, where E is the number of edges and V is the number of vertices.
  - Kruskal's algorithm has a time complexity of **O(E log E)**, which is generally faster for large graphs.

- **Space complexity**
  - Both algorithms have a space complexity of O(V), as they need to store information about each vertex (i.e., its parent in the MST).

In summary, Prim's algorithm starts with an arbitrary vertex, grows the MST from that vertex, and selects edges based on their weight, while Kruskal's algorithm processes all edges in the graph, selects edges based on their weight, and performs union operations for each connected component.
