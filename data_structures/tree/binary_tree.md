# Binary Tree
A binary tree is a type of tree data structure in which each node has at most two child nodes, typically referred to as the left child and the right child.

## Characteristics
- Each node has at most two child nodes.
- No cycles: A binary tree does not contain any cycles (or loops). Each node's left and right child nodes are distinct and do not reference the same node.
- Root node: Every binary tree has a root node, which is the topmost node in the tree.

## Balanced Binary Tree
A balanced binary tree is a binary tree where the height of the left and right subtrees of every node differs by at most one. This means that the tree is roughly equally balanced on both sides, which makes it more efficient for search, insert, and delete operations.
- Height balance: The height of the left subtree and the height of the right subtree of every node differ by at most one.
- Self-balancing: When an operation (insert, delete) is performed on the tree, it adjusts itself to maintain the balancing property.
- No nodes with more than two children: Each node has at most two child nodes, which makes the tree a binary tree.

### Example of Balanced Binary Tree
- AVL Tree
- Red-Black Tree
- B-Tree

## Perfect Tree (Full Tree or Complete Tree)
A perfect tree is a tree data structure where every internal node has two child nodes, and all leaf nodes are at the same depth. In other words, a perfect tree is a complete binary tree.
- All internal nodes have exactly two children.
- All leaf nodes (also called external nodes) are at the same depth.
- The number of nodes at each level increases by a factor of 2.

## Binary Search Tree (BST)
A binary search tree is a type of binary tree that satisfies the following conditions:
- All elements in the left subtree are less than the parent node: In a BST, all nodes to the left of a given node have values less than the value of that node.
- All elements in the right subtree are greater than the parent node: Similarly, all nodes to the right of a given node have values greater than the value of that node.
- Each node has at most two child nodes: Like any binary tree, a BST has no more than two child nodes per node.

## Implementation
### C++ Implementation
```c++
// Node structure for the BST
struct Node {
    int value;
    Node* left;
    Node* right;
};

class BinarySearchTree {
public:
    // Constructor to create an empty BST
    BinarySearchTree() : root(nullptr) {}

    // Method to insert a new node into the BST
    void insert(int value) {
        Node* newNode = new Node();
        newNode->value = value;
        newNode->left = nullptr;
        newNode->right = nullptr;

        if (root == nullptr || value < root->value) {
            // If the tree is empty or the new node's value is less than the root's, insert to the left
            if (root == nullptr) {
                root = newNode;
            } else {
                Node* current = root;
                while (current->left != nullptr && value < current->value) {
                    current = current->left;
                }
                current->left = newNode;
            }
        } else {
            // If the new node's value is greater than or equal to the root's, insert to the right
            Node* current = root;
            while (current->right != nullptr && value >= current->value) {
                current = current->right;
            }
            current->right = newNode;
        }
    }

    // Method to search for a node with a given value in the BST
    bool search(int value) {
        Node* current = root;
        while (current != nullptr) {
            if (value < current->value) {
                current = current->left;
            } else if (value > current->value) {
                current = current->right;
            } else {
                return true; // Found the node
            }
        }
        return false; // Not found
    }

private:
    Node* root;
};
```

### Golang Implementation
```Golang
// Node structure for the BST
type Node struct {
    value int
    left *Node
    right *Node
}

func (bst *BinarySearchTree) insert(value int) {
    node := &Node{value: value, left: nil, right: nil}
    if bst.root == nil || value < bst.root.value {
        // If the tree is empty or the new node's value is less than the root's, insert to the left
        if bst.root == nil {
            bst.root = node
        } else {
            current := &bst.root
            for ; current.left != nil && value < current.value; current = current.left {}
            current.left = node
        }
    } else {
        // If the new node's value is greater than or equal to the root's, insert to the right
        current := &bst.root
        for ; current.right != nil && value >= current.value; current = current.right {}
        current.right = node
    }
}

func (bst *BinarySearchTree) search(value int) bool {
    current := &bst.root
    for ; current != nil; {
        if value < current.value {
            current = &current.left
        } else if value > current.value {
            current = &current.right
        } else {
            return true // Found the node
        }
    }
    return false // Not found
}

type BinarySearchTree struct {
    root *Node
}
```

### Python Implementation
```python
class Node:
    """A node in the binary search tree."""
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


class BinarySearchTree:
    """A binary search tree (BST) implementation."""
    def __init__(self):
        self.root = None

    def insert(self, key):
        """Insert a new key into the BST."""
        if self.root is None:
            self.root = Node(key)
        else:
            self._insert(self.root, key)

    def _insert(self, current, key):
        if key < current.key:
            if current.left is None:
                current.left = Node(key)
            else:
                self._insert(current.left, key)
        elif key > current.key:
            if current.right is None:
                current.right = Node(key)
            else:
                self._insert(current.right, key)

    def search(self, key):
        """Search for a key in the BST. Returns True if found, otherwise False."""
        return self._search(self.root, key)

    def _search(self, current, key):
        if current is None:
            return False
        if key == current.key:
            return True
        elif key < current.key:
            return self._search(current.left, key)
        else:
            return self._search(current.right, key)

    def inorder_traversal(self):
        """Perform an inorder traversal of the BST."""
        result = []
        self._inorder_traversal(self.root, result)
        return result

    def _inorder_traversal(self, current, result):
        if current is not None:
            self._inorder_traversal(current.left, result)
            result.append(current.key)
            self._inorder_traversal(current.right, result)


# Example usage:
bst = BinarySearchTree()
bst.insert(50)
bst.insert(30)
bst.insert(70)
bst.insert(20)
bst.insert(40)
bst.insert(60)
bst.insert(80)

print("Inorder Traversal:", bst.inorder_traversal())  # Outputs: [20, 30, 40, 50, 60, 70, 80]
print("Search 40:", bst.search(40))  # Outputs: True
print("Search 25:", bst.search(25))  # Outputs: False
```

## Leetcode Questions
1. Binary Search Tree
- [270 Closest Binary Search Tree Value](../leetcode_questions/270_closest_binary_search_tree_value.md)
- [450 Delete Node in BST](../leetcode_questions/450_delete_node_in_BST.md)
- [98 Validate Binary Search Tree](../leetcode_questions/98_validate_binary_search_tree.md)
- [173 Binary Search Tree Iterator](../leetcode_questions/173_binary_search_tree_iterator.md)
- [99 Recover Binary Search Tree](../leetcode_questions/99_recover_binary_search_tree.md)
- [108 Convert Sorted Array to Binary Search Tree](../leetcode_questions/108_convert_sorted_array_to_binary_search_tree.md)
- [1382 Balance a Binary Search Tree](../leetcode_questions/1382_balance_a_binary_search_tree.md)
- [96 Unique Binary Search Trees](../leetcode_questions/96_unique_binary_search_trees.md)
- [95 Unique Binary Search Trees II](../leetcode_questions/95_unique_binary_search_trees_ii.md)
- [450 Delete Node in a BST](../leetcode_questions/450_delete_node_in_BST.md)

2. Lowest Common Ancestor
- [235 Lowest Common Ancestor of a Binary Search Tree](../leetcode_questions/235_lowest_common_ancestor_of_a_binary_search_tree.md)
- [236 Lowest Common Ancestor of a Binary Tree](../leetcode_questions/236_lowest_common_ancestor_of_a_binary_tree.md)
- [1644 Lowest Common Ancestor of a Binary Tree II](../leetcode_questions/1644_lowest_common_ancestor_of_a_binary_tree_ii.md)
- [1650 Lowest Common Ancestor of a Binary Tree III](../leetcode_questions/1650_lowest_common_ancestor_of_a_binary_tree_iii.md)
- [1676 Lowest Common Ancestor of a Binary Tree IV](../leetcode_questions/1676_lowest_common_ancestor_of_a_binary_tree_iv.md)
- [1123 Lowest Common Ancestor of Deepest Leaves](../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md)
- [865 Smallest Subtree with all the Deepest Nodes](../leetcode_questions/865_smallest_subtree_with_all_the_deepest_nodes.md)