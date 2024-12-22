# Graph Search

Searching in a graph data structure involves finding all nodes that satisfy certain conditions. 

## I. Breadth-First Search (BFS)

BFS starts at a given node and explores all its neighbors before moving on to the next level of nodes. It's useful for finding the shortest path between two nodes.

### C++ Implementation
```c++
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

struct Node {
    int val;
    vector<Node*> neighbors;
};

void BFS(Node* start, vector<Node*>& nodes) {
    queue<Node*> q;
    vector<bool> visited(nodes.size(), false);

    q.push(start);
    visited[start->val] = true;

    while (!q.empty()) {
        Node* node = q.front();
        q.pop();

        cout << node->val << " ";

        for (Node* neighbor : node->neighbors) {
            if (!visited[neighbor->val]) {
                q.push(neighbor);
                visited[neighbor->val] = true;
            }
        }
    }
}

int main() {
    int numNodes = 6;
    vector<Node*> nodes(numNodes);

    // Create nodes and edges
    nodes[0].val = 0;
    nodes[1].val = 1;
    nodes[2].val = 2;
    nodes[3].val = 3;
    nodes[4].val = 4;
    nodes[5].val = 5;

    nodes[0].neighbors.push_back(&nodes[1]);
    nodes[0].neighbors.push_back(&nodes[2]);
    nodes[1].neighbors.push_back(&nodes[3]);
    nodes[2].neighbors.push_back(&nodes[4]);
    nodes[4].neighbors.push_back(&nodes[5]);

    // Run BFS from node 0
    BFS(&nodes[0], nodes);

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
    "fmt"
)

// Node represents a node in the graph
type Node struct {
    val       int
    neighbors []*Node
}

// BFS performs a breadth-first search starting from the given node
func BFS(start *Node, nodes []*Node) {
    // Initialize the queue with the starting node
    queue := make([]*Node, 0)
    queue = append(queue, start)

    // Initialize the visited map
    visited := make(map[*Node]bool)
    visited[start] = true

    // Loop until the queue is empty
    for len(queue) > 0 {
        // Dequeue a node from the front of the queue
        node := queue[0]
        queue = queue[1:]

        // Process the current node
        fmt.Println(node.val)

        // Enqueue all unvisited neighbors
        for _, neighbor := range node.neighbors {
            if !visited[neighbor] {
                queue = append(queue, neighbor)
                visited[neighbor] = true
            }
        }
    }
}

func main() {
    // Create nodes
    numNodes := 6
    nodes := make([]*Node, numNodes)
    for i := range nodes {
        nodes[i] = &Node{val: i}
    }

    // Define neighbors
    nodes[0].neighbors = append(nodes[0].neighbors, nodes[1], nodes[2])
    nodes[1].neighbors = append(nodes[1].neighbors, nodes[3])
    nodes[2].neighbors = append(nodes[2].neighbors, nodes[4])
    nodes[4].neighbors = append(nodes[4].neighbors, nodes[5])

    // Run BFS from node 0
    BFS(nodes[0], nodes)
}
```

### Python Implementation
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.neighbors = []

def bfs(start):
    # Initialize the queue with the starting node
    queue = [start]

    # Initialize the visited set
    visited = set()
    visited.add(start)

    # Loop until the queue is empty
    while queue:
        # Dequeue a node from the front of the queue
        node = queue.pop(0)

        # Process the current node
        print(node.val)

        # Enqueue all unvisited neighbors
        for neighbor in node.neighbors:
            if neighbor not in visited:
                queue.append(neighbor)
                visited.add(neighbor)

# Main code
if __name__ == "__main__":
    # Create nodes
    num_nodes = 6
    nodes = [Node(i) for i in range(num_nodes)]

    # Define neighbors
    nodes[0].neighbors.extend([nodes[1], nodes[2]])
    nodes[1].neighbors.extend([nodes[3]])
    nodes[2].neighbors.extend([nodes[4]])
    nodes[4].neighbors.extend([nodes[5]])

    # Run BFS from node 0
    bfs(nodes[0])
```

## II. Depth-First Search (DFS)

DFS also starts at a given node and explores as far as possible along each branch before backtracking.

### C++ Implementation
```c++
#include <iostream>
#include <vector>
using namespace std;

struct Node {
    int val;
    vector<Node*> neighbors;
};

void DFS(Node* start, vector<Node*>& nodes) {
    stack<Node*> stack;
    vector<bool> visited(nodes.size(), false);

    stack.push(start);
    visited[start->val] = true;

    while (!stack.empty()) {
        Node* node = stack.top();
        stack.pop();

        cout << node->val << " ";

        for (Node* neighbor : node->neighbors) {
            if (!visited[neighbor->val]) {
                stack.push(neighbor);
                visited[neighbor->val] = true;
            }
        }
    }
}

int main() {
    int numNodes = 6;
    vector<Node*> nodes(numNodes);

    // Create nodes and edges
    for (int i = 0; i < numNodes; i++) {
        nodes[i]->val = i;
    }

    nodes[0]->neighbors.push_back(&nodes[1]);
    nodes[0]->neighbors.push_back(&nodes[2]);
    nodes[1]->neighbors.push_back(&nodes[3]);
    nodes[2]->neighbors.push_back(&nodes[4]);
    nodes[4]->neighbors.push_back(&nodes[5]);

    // Run DFS from node 0
    DFS(&nodes[0], nodes);

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
	"fmt"
	"sync"
)

// Node represents a node in the graph
type Node struct {
	val       int
	neighbors []*Node
}

// DFS performs a depth-first search starting from the given node
func DFS(start *Node, nodes []*Node) {
	stack := []*Node{}
	visited := make([]bool, len(nodes))

	stack = append(stack, start)
	visited[start.val] = true

	for len(stack) > 0 {
		// Pop a node from the stack
		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		// Process the current node
		fmt.Printf("%d ", node.val)

		// Visit all unvisited neighbors
		for _, neighbor := range node.neighbors {
			if !visited[neighbor.val] {
				stack = append(stack, neighbor)
				visited[neighbor.val] = true
			}
		}
	}
}

func main() {
	numNodes := 6
	nodes := make([]*Node, numNodes)

	// Create nodes
	for i := 0; i < numNodes; i++ {
		nodes[i] = &Node{val: i}
	}

	// Define neighbors
	nodes[0].neighbors = append(nodes[0].neighbors, nodes[1], nodes[2])
	nodes[1].neighbors = append(nodes[1].neighbors, nodes[3])
	nodes[2].neighbors = append(nodes[2].neighbors, nodes[4])
	nodes[4].neighbors = append(nodes[4].neighbors, nodes[5])

	// Run DFS from node 0
	DFS(nodes[0], nodes)
}
```

### Python Implementation
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.neighbors = []

def dfs(start, num_nodes):
    # Initialize the stack and visited list
    stack = [start]
    visited = [False] * num_nodes

    visited[start.val] = True

    while stack:
        # Pop a node from the stack
        node = stack.pop()

        # Process the current node
        print(node.val, end=" ")

        # Visit all unvisited neighbors
        for neighbor in node.neighbors:
            if not visited[neighbor.val]:
                stack.append(neighbor)
                visited[neighbor.val] = True

# Main code
if __name__ == "__main__":
    num_nodes = 6
    nodes = [Node(i) for i in range(num_nodes)]

    # Define neighbors
    nodes[0].neighbors.extend([nodes[1], nodes[2]])
    nodes[1].neighbors.extend([nodes[3]])
    nodes[2].neighbors.extend([nodes[4]])
    nodes[4].neighbors.extend([nodes[5]])

    # Run DFS from node 0
    dfs(nodes[0], num_nodes)
```

## III. Runtime Complexity
### Using an Adjacency List

When a graph is represented using an adjacency list, the runtime complexity of BFS is **O(V + E)**,
V is the number of vertices (nodes) in the graph. E is the number of edges in the graph.

It is because each vertex is visited at most once, leading to O(V) operations for vertices.
Each edge is considered once when exploring the neighbors of a vertex, leading to O(E) operations for edges.
Thus, the total time complexity is **O(V + E)**.

### Using an Adjacency Matrix

When a graph is represented using an adjacency matrix, the runtime complexity of BFS is **O(V^2)**. This is because:

Each vertex is visited at most once, leading to O(V) operations for vertices. **Checking all possible neighbors for each vertex requires O(V) time**, resulting in **O(V^2)** operations to explore all edges.

### Summary

DFS Time Complexity: **O(V + E)** or **O(V^2)**

BFS Time Complexity: **O(V + E)** or **O(V^2)**

DFS Space Complexity: **O(V)**

BFS Space Complexity: **O(V)**

## Leetcode Questions
- [127. Word Ladder]()
- [130. Surrounded Regions]()
- [133. Clone Graph]() 
- [200. Number of Islands]()
- [417. Pacific Atlantic Water Flow]()
- [797. All Paths From Source to Target]()
- [994. Rotting Oranges]()
