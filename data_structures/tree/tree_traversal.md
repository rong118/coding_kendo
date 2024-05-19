# Tree Traversal

There are several ways to traverse a tree data structure, depending on the order in which you want to visit the nodes

## Pre-order traversal
Visit the current node first, then recursively traverse the left subtree, and finally traverse the right subtree.

Example: In a binary tree, visit the root node, then the left child, then the right child.

### C++ Implementation
```c++
#include <iostream>
using namespace std;

struct Node {
    int value;
    struct Node* left;
    struct Node* right;
};

void preorder(struct Node* node) {
    if (node == NULL)
        return;

    cout << node->value << " ";

    preorder(node->left);
    preorder(node->right);
}

int main() {
    // Create a sample tree
    struct Node* root = new struct Node();
    root->value = 1;
    root->left = new struct Node();
    root->left->value = 2;
    root->right = new struct Node();
    root->right->value = 3;
    root->left->left = new struct Node();
    root->left->left->value = 4;
    root->left->right = new struct Node();
    root->left->right->value = 5;

    // Perform pre-order traversal
    preorder(root);

    return 0;
}
```

```golang
package main

import (
    "fmt"
)

type Node struct {
    value int
    left  *Node
    right *Node
}

func preorder(node *Node) {
    if node == nil {
        return
    }

    fmt.Println(node.value)
    preorder(node.left)
    preorder(node.right)
}

func main() {
    // Create a sample tree
    root := &Node{1, nil, nil}
    leftChild := &Node{2, nil, nil}
    rightChild := &Node{3, nil, nil}
    grandLeftChild := &Node{4, nil, nil}
    grandRightChild := &Node{5, nil, nil}

    root.left = leftChild
    root.right = rightChild
    leftChild.left = grandLeftChild
    leftChild.right = grandRightChild

    // Perform pre-order traversal
    preorder(root)
}
```

## In-order traversal
Traverse the left subtree, then visit the current node, and finally traverse the right subtree.

Example: In a binary tree, visit the left child of the root, then the root itself, then the right child.

### C++
```c++
#include  <iostream>
using namespace std;

struct Node {
    int value;
    struct Node* left;
    struct Node* right;
};

void inorder(struct Node* node) {
    if (node == NULL)
        return;

    inorder(node->left);

    cout << node->value << " ";

    inorder(node->right);
}

int main() {
    // Create a sample tree
    struct Node* root = new struct Node();
    root->value = 1;
    root->left = new struct Node();
    root->left->value = 2;
    root->right = new struct Node();
    root->right->value = 3;
    root->left->left = new struct Node();
    root->left->left->value = 4;
    root->left->right = new struct Node();
    root->left->right->value = 5;

    // Perform in-order traversal
    inorder(root);

    return 0;
}
```

### Golang
```golang
package main

import (
    "fmt"
)

type Node struct {
    value int
    left  *Node
    right *Node
}

func inorder(node *Node) {
    if node == nil {
        return
    }

    inorder(node.left)
    fmt.Println(node.value, " ")
    inorder(node.right)
}

func main() {
    // Create a sample tree
    root := &Node{1, nil, nil}
    leftChild := &Node{2, nil, nil}
    rightChild := &Node{3, nil, nil}
    grandLeftChild := &Node{4, nil, nil}
    grandRightChild := &Node{5, nil, nil}

    root.left = leftChild
    root.right = rightChild
    leftChild.left = grandLeftChild
    leftChild.right = grandRightChild

    // Perform in-order traversal
    inorder(root)
}
```

## Post-order traversal
Traverse the left subtree, then traverse the right subtree, and finally visit the current node.

Example: In a binary tree, visit the left child of the root, then the right child, then the root itself.

### C++
```c++
#include   <iostream>
using namespace std;

struct Node {
    int value;
    struct Node* left;
    struct Node* right;
};

void postorder(struct Node* node) {
    if (node == NULL)
        return;

    postorder(node->left);
    postorder(node->right);

    cout << node->value << " ";
}

int main() {
    // Create a sample tree
    struct Node* root = new struct Node();
    root->value = 1;
    root->left = new struct Node();
    root->left->value = 2;
    root->right = new struct Node();
    root->right->value = 3;
    root->left->left = new struct Node();
    root->left->left->value = 4;
    root->left->right = new struct Node();
    root->left->right->value = 5;

    // Perform post-order traversal
    postorder(root);

    return 0;
}
```

### Golang
```golang
package main

import (
    "fmt"
)

type Node struct {
    value int
    left  *Node
    right *Node
}

func postorder(node *Node) {
    if node == nil {
        return
    }

    postorder(node.left)
    postorder(node.right)

    fmt.Println(node.value, " ")
}

func main() {
    // Create a sample tree
    root := &Node{1, nil, nil}
    leftChild := &Node{2, nil, nil}
    rightChild := &Node{3, nil, nil}
    grandLeftChild := &Node{4, nil, nil}
    grandRightChild := &Node{5, nil, nil}

    root.left = leftChild
    root.right = rightChild
    leftChild.left = grandLeftChild
    leftChild.right = grandRightChild

    // Perform post-order traversal
    postorder(root)
}
```

## Runtime Complexity
The runtime complexity of traversing a binary tree (pre-order, in-order, or post-order) is **O(n)**, where n is the number of nodes in the tree. 

This is because, in each traversal method, every node in the tree is visited exactly once

## Leetcode Questions
1. 遍历
- [144 Binary Tree Preorder Traversal](../../leetcode_questions/144_binary_tree_preorder_traversal.md)
- [94 Binary Tree Inorder Traversal](../../leetcode_questions/94_binary_tree_inorder_traversal.md)
- [145 Binary Tree Postorder Traversal](../../leetcode_questions/145_binary_tree_postorder_traversal.md)
- [102 Binary Tree Level Order Traversal](../../leetcode_questions/102_binary_tree_level_order_traversal.md)
- [103 Binary Tree Zigzig Level Order Traversal](../../leetcode_questions/103_binary_tree_zigzig_level_order_traversal.md)
- [107 Binary Tree Level Order Traversal II](../../leetcode_questions/107_binary_tree_level_order_traversal_II.md)
- [314 Binary Tree Vertical Order Traversal](../../leetcode_questions/314_binary_tree_vertical_order_traversal.md)
- [987 Vertical Order Traversal of a Binary Tree](../../leetcode_questions/987_vertical_order_traversal_of_a_binary_tree.md)

2. 结构转换/序列化
- [297 Serialize and Deserialize Binary Tree](../../leetcode_questions/297_serialize_and_deserialize_binary_tree.md)
- [428 Serialize and Deserialize N-ary Tree](../../leetcode_questions/428_serialize_and_deserialize_nary_tree.md)
- [449 Serialize and Deserialize BST](../../leetcode_questions/449_serialize_and_deserialize_BST.md)
- [1008 Construct Binary Search Tree from Preorder Traversal](../../leetcode_questions/1008_construct_binary_search_tree_from_preorder_traversal.md)
- [105 Construct Binary Tree from Preorder and Inorder Traversal](../../leetcode_questions/105_construct_binary_tree_from_preorder_and_inorder_traversal.md)
- [106 Construct Binary Tree from Inorder and Postorder Traversal](../../leetcode_questions/106_construct_binary_tree_from_inorder_and_postorder_traversal.md)
- [889 Construct Binary Tree from Preorder and Postorder Traversal](../../leetcode_questions/889_construct_binary_tree_from_preorder_and_postorder_traversal.md)
- [426 Convert Binary Search Tree to Sorted Doubly Linked List](../../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md)