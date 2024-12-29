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
```python
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        
        # Initialize a num_vertices x num_vertices matrix with all zeros
        self.adj_matrix = [[0] * num_vertices for _ in range(num_vertices)]

    def add_edge(self, src, dest, weight=1):
        """Add an edge to the graph."""
        if src < 0 or src >= self.num_vertices or dest < 0 or dest >= self.num_vertices:
            print("Error: Invalid vertex number")
            return
        self.adj_matrix[src][dest] = weight
        self.adj_matrix[dest][src] = weight  # For undirected graphs

    def remove_edge(self, src, dest):
        """Remove an edge from the graph."""
        if src < 0 or src >= self.num_vertices or dest < 0 or dest >= self.num_vertices:
            print("Error: Invalid vertex number")
            return
        self.adj_matrix[src][dest] = 0
        self.adj_matrix[dest][src] = 0  # For undirected graphs

    def display(self):
        """Display the adjacency matrix."""
        for row in self.adj_matrix:
            print(row)

# Example usage:
if __name__ == "__main__":
    num_vertices = 5
    graph = Graph(num_vertices)

    # Add some edges
    graph.add_edge(0, 1)
    graph.add_edge(0, 4, 2)
    graph.add_edge(1, 2)
    graph.add_edge(1, 3)
    graph.add_edge(3, 4)

    # Display the adjacency matrix
    print("Adjacency Matrix:")
    graph.display()

    # Remove an edge
    print("\nRemoving edge between vertex 1 and vertex 3...")
    graph.remove_edge(1, 3)

    # Display the updated adjacency matrix
    print("Updated Adjacency Matrix:")
    graph.display()
```

### Adjacency List
```python
class Graph:
    def __init__(self):
        self.adj_list = {}

    def add_edge(self, src, dest, weight=1, directed=False):
        """Add an edge to the graph."""
        if src not in self.adj_list:
            self.adj_list[src] = []
        if dest not in self.adj_list:
            self.adj_list[dest] = []
        
        # Add the edge
        self.adj_list[src].append((dest, weight))
        if not directed:
            self.adj_list[dest].append((src, weight))

    def remove_edge(self, src, dest, directed=False):
        """Remove an edge from the graph."""
        if src in self.adj_list:
            self.adj_list[src] = [(d, w) for d, w in self.adj_list[src] if d != dest]
        if not directed and dest in self.adj_list:
            self.adj_list[dest] = [(s, w) for s, w in self.adj_list[dest] if s != src]

    def display(self):
        """Display the adjacency list."""
        for vertex, edges in self.adj_list.items():
            print(f"{vertex}: {edges}")

# Example usage:
if __name__ == "__main__":
    graph = Graph()

    # Add some edges
    graph.add_edge(0, 1)
    graph.add_edge(0, 3, 2)
    graph.add_edge(1, 2)

    # Display the adjacency list
    print("Adjacency List:")
    graph.display()

    # Remove an edge
    print("\nRemoving edge between vertex 1 and vertex 3...")
    graph.remove_edge(1, 2)

    # Display the updated adjacency list
    print("Updated Adjacency List:")
    graph.display()
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
