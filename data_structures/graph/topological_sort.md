# Topological Sort

Topological sorting is a linear ordering of vertices in a **directed acyclic graph (DAG)** such that for every directed edge u→v, vertex u comes before v in the ordering.

## key characteristics

### - Ordering:

TS produces a linear ordering of the vertices in a directed acyclic graph (DAG), such that for every edge (u, v), vertex u comes before vertex v in the ordering.

### - No Cycles:

TS only works on DAGs, meaning there are no cycles in the graph. If a cycle is present, the algorithm will not be able to produce a valid topological ordering.

### - Not Necessarily Unique:

TS may not always produce a unique ordering for a given graph. This is because there may be multiple valid topological orderings for a graph that has multiple DAGs as subgraphs.

### - Can Be Used for Scheduling:

One of the most common applications of Topological Sort is in scheduling, where it can be used to schedule tasks or jobs based on their dependencies.

## Implementation

### Using Depth-First Search (DFS):

```c++
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Function to perform DFS and push vertices to the stack
void topologicalSortUtil(int v, vector<bool>& visited, stack<int>& Stack, const vector<vector<int>>& adj) {
    visited[v] = true;  // Mark the current node as visited

    // Recur for all the vertices adjacent to this vertex
    for (int i : adj[v]) {
        if (!visited[i]) {
            topologicalSortUtil(i, visited, Stack, adj);
        }
    }

    // Push current vertex to stack which stores the result
    Stack.push(v);
}

// Function to perform topological sort
vector<int> topologicalSort(int V, const vector<vector<int>>& adj) {
    stack<int> Stack;
    vector<bool> visited(V, false);
    vector<int> result;

    // Call the recursive helper function to store Topological Sort starting from all vertices one by one
    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            topologicalSortUtil(i, visited, Stack, adj);
        }
    }

    // Pop all vertices from the stack and add to the result
    while (!Stack.empty()) {
        result.push_back(Stack.top());
        Stack.pop();
    }

    return result;
}

int main() {
    // Example graph
    int V = 6;
    vector<vector<int>> adj(V);

    // Adding edges
    adj[5].push_back(2);
    adj[5].push_back(0);
    adj[4].push_back(0);
    adj[4].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(1);

    vector<int> result = topologicalSort(V, adj);

    cout << "Topological Sort of the given graph:\n";
    for (int i : result) {
        cout << i << " ";
    }

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
    "fmt"
)

type Graph struct {
    vertices map[int][]int
}

func NewGraph() *Graph {
    return &Graph{make(map[int][]int)}
}

func (g *Graph) AddEdge(u, v int) {
    if _, ok := g.vertices[u]; !ok {
        g.vertices[u] = []int{}
    }
    g.vertices[u] = append(g.vertices[u], v)
}

func (g *Graph) TopologicalSort() ([]int, error) {
    order := []int{}
    visited := make(map[int]bool)

    for node := range g.vertices {
        if !visited[node] {
            if err := g.dfs(node, visited, &order); err != nil {
                return nil, err
            }
        }
    }

    return order, nil
}

func (g *Graph) dfs(node int, visited map[int]bool, order *[]int) error {
    if !visited[node] {
        visited[node] = true

        for _, neighbor := range g.vertices[node] {
            if !visited[neighbor] {
                if err := g.dfs(neighbor, visited, order); err != nil {
                    return err
                }
            } else if contains(g.vertices[neighbor], node) {
                return fmt.Errorf("cycle detected: %d", node)
            }
        }

    *order = append(*order, node)
    } else if !g.hasNoIncomingEdges(node) {
        return fmt.Errorf("cycle detected: %d", node)
    }

    return nil
}

func (g *Graph) hasNoIncomingEdges(node int) bool {
    for neighbor := range g.vertices {
        if contains(g.vertices[neighbor], node) {
            return false
        }
    }
    return true
}

func contains(slice []int, val int) bool {
    for _, v := range slice {
        if v == val {
            return true
        }
    }
    return false
}

func main() {
    g := NewGraph()
    g.AddEdge(0, 1)
    g.AddEdge(1, 2)
    g.AddEdge(2, 3)
    g.AddEdge(3, 4)

    order, err := g.TopologicalSort()

    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Println(order) // [0 1 2 3 4]
}
```

## Runtime Complexity:

### - Depth-First Search (DFS) Based Topological Sort

Each vertex is visited exactly once, marking it as visited. This contributes **O(V)** to the complexity.
For each vertex, all its adjacent vertices (edges) are explored. This traversal of all edges contributes **O(E)** to the complexity.
Thus, the total complexity for the DFS-based topological sort is **O(V+E)**.
