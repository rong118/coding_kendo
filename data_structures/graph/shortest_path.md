# Shortest Path

The Shortest Path Problem is a fundamental problem in graph theory. Given a weighted graph, the goal is to find the shortest path between two nodes (also known as vertices) that minimizes the sum of edge weights.

## Common Algorithms
- Dijkstra's Algorithm
- Bellman-Ford Algorithm

## Dijkstra's Algorithm

A greedy algorithm works by maintaining a priority queue of nodes, where the priority is the minimum distance from the source node to each node.

### C++ Implementation
```c++
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

struct Edge {
    int u, v, w;
};

class Graph {
public:
    vector<Edge> edges;
    int V; // number of vertices

    Graph(int V) : V(V) {}

    void addEdge(int u, int v, int w) {
        edges.push_back({u, v, w});
    }

    vector<int> dijkstra(int src) {
        vector<int> dist(V, INT_MAX);
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        dist[src] = 0;
        pq.push({0, src});

        while (!pq.empty()) {
            int u = pq.top().second;
            pq.pop();
            for (Edge& e : edges) {
                if (e.u == u && dist[e.v] > dist[u] + e.w) {
                    dist[e.v] = dist[u] + e.w;
                    pq.push({dist[e.v], e.v});
                }
            }
        }

        return dist;
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1, 4);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 2, 2);
    g.addEdge(1, 3, 10);
    g.addEdge(2, 1, 8);
    g.addEdge(2, 3, 5);
    g.addEdge(3, 4, 7);

    vector<int> dist = g.dijkstra(0);

    for (int i = 0; i < 5; i++) {
        cout << "Distance from node 0 to node " << i << ": " << dist[i] << endl;
    }

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
    "fmt"
    "container/heap"
)

type Edge struct {
    u, v int
    w int
}

type Graph struct {
    edges []Edge
    V int // number of vertices
}

func (g *Graph) addEdge(u, v int, w int) {
    g.edges = append(g.edges, Edge{u, v, w})
}

func (g *Graph) dijkstra(src int) []int {
    dist := make([]int, g.V)
    pq := &heap.IntHeap{}
    dist[src] = 0
    pq.Init()
    pq.Push(0, src)

    for pq.Len() > 0 {
        u := pq.Pop().(0)
        for _, e := range g.edges {
            if e.u == u && dist[e.v] > dist[u] + e.w {
                dist[e.v] = dist[u] + e.w
                pq.Push(dist[e.v], e.v)
            }
        }
    }

    return dist
}

func main() {
    g := &Graph{V: 5}
    g.addEdge(0, 1, 4)
    g.addEdge(0, 2, 3)
    g.addEdge(1, 2, 2)
    g.addEdge(1, 3, 10)
    g.addEdge(2, 1, 8)
    g.addEdge(2, 3, 5)
    g.addEdge(3, 4, 7)

    dist := g.dijkstra(0)

    for i := 0; i < 5; i++ {
        fmt.Println("Distance from node 0 to node", i, ":", dist[i])
    }
}
```

### Runtime Complexity

The time complexity of Dijkstra's Algorithm is **O(|E|log|V|)** in the worst case, where: |E| is the number of edges in the graph. |V| is the number of vertices (nodes) in the graph.

This is because the algorithm uses a priority queue to keep track of nodes to visit, and the priority queue operations (insertion and extraction) take O(log|V|) time. The loop iterates over all edges, so it takes O(|E|) time. Therefore, the total time complexity is **O(|E|log|V|)**.

## Bellman-Ford Algorithm: 

A modification of Dijkstra's Algorithm that handles negative weight edges. It's particularly useful for graphs with negative cycles, which can cause Dijkstra's Algorithm to fail.

### C++ Implmentation
```c++
#include  <iostream>
#include  <vector>

using namespace std;

struct Edge {
    int u, v; // nodes
    int w;     // weight (can be negative)
};

class Graph {
public:
    vector<Edge> edges;
    int V; // number of vertices

    void addEdge(int u, int v, int w) {
        edges.push_back({u, v, w});
    }

    vector<int> bellmanFord(int src) {
        vector<int> dist(V, INT_MAX); // distances from source to all nodes
        dist[src] = 0;               // distance to source is 0

        for (int i = 0; i < V - 1; i++) { // relax edges |V-1| times
            for (auto &e : edges) {
                int u = e.u, v = e.v, w = e.w;
                if (dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                }
            }
        }

        return dist;
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1, -2); // negative weight edge
    g.addEdge(1, 2, 3);   // positive weight edge
    g.addEdge(2, 3, 2);   // positive weight edge
    g.addEdge(3, 4, -1);  // negative weight edge
    g.addEdge(4, 0, 2);   // positive weight edge

    vector<int> dist = g.bellmanFord(0);

    cout << "Shortest distances from node 0:" << endl;
    for (int i = 0; i < V; i++) {
        cout << "Node " << i << ": " << dist[i] << endl;
    }

    return 0;
}
```

### Key points

- The algorithm can handle negative weight edges, which Dijkstra' s Algorithm cannot.
- It uses the same priority queue operations as Dijkstra' s Algorithm.
- The time complexity is **O(|E| * |V|)**, where |E| is the number of edges and |V| is the number of vertices.

## Leetcode Questions
- [787 Cheapest Flights Within K Stops](../leetcode_questions/787_cheapest_flights_within_k_stops.md)