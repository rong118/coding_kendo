# Graph

A graph is a non-linear data structure consisting of nodes (also called vertices) connected by edges. Each node represents an entity or object, and the edges represent relationships between these entities.

## Key characteristics:
- **Nodes (Vertices)**: A graph consists of a set of nodes, which are also referred to as vertices.
- **Edges**: The edges connect the nodes, representing relationships between them.
- **Directionality**: Edges can be directed (one-way) or undirected (two-way).
- **Weightedness**: Edges can have weights or labels attached to them, which represent additional information about the relationship.


## Graph Representations:
- **Adjacency Matrix**: A matrix where the entry at row i and column j represents whether there is an edge between node i and node j.
- **Adjacency List**: A list of edges, where each edge is represented as a pair of nodes.

## Graph Operations:
- **Traversals**: Methods to visit all nodes in the graph, such as DFS (Depth-First Search), BFS (Breadth-First Search), and Topological Sort.
- **Shortest Path**: Finding the shortest path between two nodes in the graph.
- **Minimum Spanning Tree**: Finding a subgraph with the minimum total weight or cost that connects all nodes.

## Implementation 
### Adjacency Matrix
#### - C++
```c++
#include <iostream>
#include <vector>

using namespace std;

class Graph {
public:
    int numNodes;
    vector<vector<int>> adjacencyMatrix;

    // Constructor to initialize the graph with a specified number of nodes
    Graph(int numNodes) {
        this->numNodes = numNodes;
        adjacencyMatrix.resize(numNodes, vector<int>(numNodes, 0));
    }

    // Function to add an edge between two nodes (assuming 0-based indexing)
    void addEdge(int node1, int node2) {
        adjacencyMatrix[node1][node2] = 1; // Directed edge from node1 to node2
        if (node2 != node1) { // Undirected edge
            adjacencyMatrix[node2][node1] = 1;
        }
    }

    // Function to print the adjacency matrix
    void printGraph() {
        for (int i = 0; i < numNodes; ++i) {
            for (int j = 0; j < numNodes; ++j) {
                cout << adjacencyMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph graph(4); // Create a graph with 4 nodes
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 3);

    graph.printGraph();

    return 0;
}
```
#### - Golang
```golang
package main

import (
    "fmt"
)

type Graph struct {
    nodes int
    matrix [][]int
}

func (g *Graph) addEdge(node1, node2 int) {
    g.matrix[node1][node2] = 1 // Directed edge from node1 to node2
    if node2 != node1 { // Undirected edge
        g.matrix[node2][node1] = 1
    }
}

func (g *Graph) printGraph() {
    for i := 0; i < g.nodes; i++ {
        for j := 0; j < g.nodes; j++ {
            fmt.Printf("%d ", g.matrix[i][j])
        }
        fmt.Println()
    }
}

func main() {
    g := &Graph{4, [][]int{{0, 0, 1, 0}, {0, 0, 0, 1}, {1, 0, 0, 1}, {0, 1, 1, 0}}}
    g.addEdge(0, 1)
    g.addEdge(0, 2)
    g.addEdge(1, 3)
    g.addEdge(2, 3)

    g.printGraph()
}
```
#### - Javascript
```javascript
class Graph {
    constructor(numNodes) {
        this.numNodes = numNodes;
        this.adjacencyMatrix = Array.from({ length: numNodes }, () => new Array(numNodes).fill(0));
    }

    addEdge(node1, node2) {
        this.adjacencyMatrix[node1][node2] = 1; // Directed edge from node1 to node2
        if (node2 !== node1) { // Undirected edge
            this.adjacencyMatrix[node2][node1] = 1;
        }
    }

    printGraph() {
        for (let i = 0; i < this.numNodes; i++) {
            for (let j = 0; j < this.numNodes; j++) {
                console.log(this.adjacencyMatrix[i][j], ' ');
            }
            console.log();
        }
    }
}

const graph = new Graph(4);
graph.addEdge(0, 1);
graph.addEdge(0, 2);
graph.addEdge(1, 3);
graph.addEdge(2, 3);

graph.printGraph();
```
### Adjacency List
#### - C++
```c++
#include <iostream>
#include <list>

class Graph {
public:
    int numNodes;
    std::vector<std::list<int>> adjacencyList;

    // Constructor to initialize the graph with a specified number of nodes
    Graph(int numNodes) : numNodes(numNodes), adjacencyList(numNodes) {}

    // Function to add an edge between two nodes (assuming 0-based indexing)
    void addEdge(int node1, int node2) {
        adjacencyList[node1].push_back(node2); // Directed edge from node1 to node2
        if (node2 != node1) { // Undirected edge
            adjacencyList[node2].push_back(node1);
        }
    }

    // Function to print the adjacency list
    void printGraph() {
        for (int i = 0; i < numNodes; ++i) {
            std::cout << "Node " << i << ": ";
            for (int j : adjacencyList[i]) {
                std::cout << j << " ";
            }
            std::cout << "\n";
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);

    g.printGraph();

    return 0;
}
```
#### - Golang
```golang
package main

import (
    "fmt"
)

type Graph struct {
    nodes int
    list [][]int
}

func (g *Graph) addEdge(node1, node2 int) {
    g.list = append(g.list, []int{node1, node2}) // Directed edge from node1 to node2
    if node2 != node1 { // Undirected edge
        g.list = append(g.list, []int{node2, node1})
} }

func (g *Graph) printGraph() {
    for i := 0; i < g.nodes; i++ {
        fmt.Printf("Node %d: ", i)
        for _, j := range g.list[i] {
            fmt.Printf("%d ", j)
    }
        fmt.Println()
}

func main() {
    g := &Graph{4, [][]int{{}, {}}}
    g.addEdge(0, 1)
    g.addEdge(0, 2)
    g.addEdge(1, 3)
    g.addEdge(2, 3)

    g.printGraph()
}
```

#### - Javascript
```javascript
class Graph {
    constructor(numNodes) {
        this.numNodes = numNodes;
        this.adjacencyList = Array.from({ length: numNodes }, () => []);

    }

    addEdge(node1, node2) {
        this.adjacencyList[node1].push(node2); // Directed edge from node1 to node2
        if (node2 !== node1) { // Undirected edge
            this.adjacencyList[node2].push(node1);
        }
    }

    printGraph() {
        for (let i = 0; i < this.numNodes; i++) {
            console.log(`Node ${i}: `);

            for (let j of this.adjacencyList[i]) {
                console.log(j, ' ');
            }
            console.log();
        }
    }
}

const graph = new Graph(4);
graph.addEdge(0, 1);
graph.addEdge(0, 2);
graph.addEdge(1, 3);
graph.addEdge(2, 3);

graph.printGraph();
```
## Adjacency Matrices vs Adjacency List

### Adjacency Matrix:
An Adjacency Matrix is a matrix where the entry at row i and column j represents whether there is an edge between node i and node j.

The matrix is typically symmetric, meaning that the entry at row i and column j is the same as the entry at row j and column i, since undirected edges are represented by both entries.

**Pros:**
  - Easy to implement: Adjacency Matrix can be implemented using a simple 2D array.
  - Fast lookup: Checking if there is an edge between two nodes is as simple as looking up the corresponding entry in the matrix, which has a time complexity of **O(1)**.
 
**Cons:**
  - Space efficiency: The space required to store the Adjacency Matrix can be large for large graphs, especially when the graph is sparse (i.e., most entries are 0).
  - Slow insertion and deletion: Adding or removing edges from the graph requires updating multiple entries in the matrix, which can be slow.

### Adjacency List:
An Adjacency List is a list of lists, where each inner list represents the nodes adjacent to a given node. This representation is often used when working with directed graphs.

**Pros:**
  - Space efficiency: The space required to store the Adjacency List is typically smaller than the Adjacency Matrix, especially for sparse graphs.
  - Fast insertion and deletion: Adding or removing edges from the graph only requires updating the corresponding inner list, which can be fast.

**Cons:**
  - Slower lookup: Checking if there is an edge between two nodes requires traversing the lists, which has a time complexity of **O(m)**, where m is the number of adjacent nodes.
  - More complex implementation: Adjacency List can be more challenging to implement than Adjacency Matrix, especially when working with large graphs or handling edge cases.

### When to use each:
  - Adjacency Matrix: Use when you need fast lookup and are working with small to medium-sized graphs where the matrix is not too large.
  - Adjacency List: Use when you need space efficiency and are working with large or sparse graphs, or when inserting and deleting edges frequently.
