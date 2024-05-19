# Tree Search

Searching a tree can be done using various algorithms, including Depth-First Search (DFS) and Breadth-First Search (BFS). 

Both DFS and BFS traverse the tree by visiting nodes in a specific order, but they differ in their approach.

## Depth-First Search (DFS)

- Start at an arbitrary node (called the "root" node).
- Visit the root node.
- Recursively visit each child of the current node until you reach a leaf node (a node with no children).
- Backtrack to the previous node and repeat the process until you return to the starting node.

### Example
```
  A
 / \
B   C
   /  \ 
   D   E
  /
  F
```
DFS would traverse this tree in the following order: A -> B -> C -> D-> F -> E

## Breadth-First Search (BFS)
- Start at an arbitrary node (called the "root" node).
- Visit all the child nodes of the root node.
- Then, visit all the grandchildren of the root node.
- Continue this process until you have visited all nodes in the tree.

### Example
```
  A
 / \
B   C
   /  \ 
   D   E
  /
  F
```
BFS would traverse this tree in the following order: A -> ( B -> C) -> (D-> E) -> F

## Key differences:
- DFS explores as far as possible along each branch before backtracking.
- BFS visits all nodes at a given level before moving on to the next level.

## Runtime Complexity
### Depth-First Search (DFS):
- Best-case scenario: O(n), where n is the number of nodes in the binary tree.
- Worst-case scenario: O(n), where n is the number of nodes in the binary tree.
- Average-case scenario: O(n), where n is the number of nodes in the binary tree.

The reason for this runtime complexity is that DFS explores as far as possible along each branch before backtracking. In a binary tree, each node has at most two children, so the maximum depth of the recursion is logarithmic (O(log n)). However, since we visit each node exactly once, the overall runtime complexity remains O(n).

### Breadth-First Search (BFS):
- Best-case scenario: O(n), where n is the number of nodes in the binary tree.
- Worst-case scenario: O(n), where n is the number of nodes in the binary tree.
- Average-case scenario: O(n), where n is the number of nodes in the binary tree.

The reason for this runtime complexity is that BFS visits all nodes at a given level before moving on to the next level. In a binary tree, each node has at most two children, so the maximum width of the queue (i.e., the number of nodes at a given level) is constant (O(1)). However, since we visit each node exactly once, the overall runtime complexity remains O(n).


## Implementation
### C++
```c++
#include <iostream>
#include <stack>
#include <queue>

using namespace std;

// Define a binary tree node structure
struct Node {
    int value;
    Node* left;
    Node* right;
};

// Function to perform DFS traversal
void dfs(Node* root) {
    stack<Node*> nodes;
    nodes.push(root);

    while (!nodes.empty()) {
        Node* current = nodes.top();
        nodes.pop();

        cout << current->value << " ";

        if (current->right != nullptr)
            nodes.push(current->right);
        if (current->left != nullptr)
            nodes.push(current->left);
    }
}

// Function to perform BFS traversal
void bfs(Node* root) {
    queue<Node*> nodes;
    nodes.push(root);

    while (!nodes.empty()) {
        Node* current = nodes.front();
        nodes.pop();

        cout << current->value << " ";

        if (current->right != nullptr)
            nodes.push(current->right);
        if (current->left != nullptr)
            nodes.push(current->left);
    }
}

int main() {
    // Create a sample binary tree
    Node* root = new Node();
    root->value = 1;
    root->left = new Node();
    root->left->value = 2;
    root->right = new Node();
    root->right->value = 3;
    root->right->left = new Node();
    root->right->left->value = 4;
    root->right->right = new Node();
    root->right->right->value = 5;

    // Perform DFS traversal
    cout << "DFS Traversal: ";
    dfs(root);
    cout << endl;

    // Perform BFS traversal
    cout << "BFS Traversal: ";
    bfs(root);
    cout << endl;

    return 0;
}
```
### Golang
```golang
package main

import (
    "fmt"
)

// Define a binary tree node structure
type Node struct {
    value int
    left  *Node
    right *Node
}

// Function to perform DFS traversal
func dfs(root *Node) {
    stack := make([]*Node, 0)
    stack = append(stack, root)

    for len(stack) > 0 {
        node := stack[len(stack)-1]
        stack = stack[:len(stack)-1]

        fmt.Println(node.value)

        if node.right != nil {
            stack = append(stack, node.right)
        }
        if node.left != nil {
            stack = append(stack, node.left)
        }
    }
}

// Function to perform BFS traversal
func bfs(root *Node) {
    queue := make([]*Node, 0)
    queue = append(queue, root)

    for len(queue) > 0 {
        node := queue[0]
        queue = queue[1:]

        fmt.Println(node.value)

        if node.right != nil {
            queue = append(queue, node.right)
        }
        if node.left != nil {
            queue = append(queue, node.left)
        }
    }
}

func main() {
    // Create a sample binary tree
    root := &Node{1, &Node{2, nil, nil}, &Node{3, &Node{4, nil, nil}, &Node{5, nil, nil}}}

    // Perform DFS traversal
    fmt.Println("DFS Traversal:")
    dfs(root)
    fmt.Println()

    // Perform BFS traversal
    fmt.Println("BFS Traversal:")
    bfs(root)
    fmt.Println()
}
```

## Leetcode Questions
1. Path (传递) => DFS (recursive)
- [257 Binary Tree Paths](../../leetcode_questions/257_binary_tree_paths.md)
- [1448 Count Good Nodes in Binary Tree](../../leetcode_questions/1448_count_good_nodes_in_binary_tree.md)
- [124 Binary Tree Maximum Path Sum](../../leetcode_questions/124_binary_tree_maximum_path_sum.md)
- [1120 Maximum Average Subtree](../../leetcode_questions/1120_maximum_average_subtree.md)
- [1372 Longest ZigZag Path in a Binary Tree](../../leetcode_questions/1372_longest_zigzag_path_in_a_binary_tree.md)
- [1123 Lowest Common Ancestor of Deepest Leaves](../../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md)
- [549 Binary Tree Longest Consecutive Sequence II](../../leetcode_questions/549_binary_tree_longest_consecutive_sequence_ii.md)