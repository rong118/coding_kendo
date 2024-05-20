# AVL Tree

An AVL tree (Adelson-Velskii and Landis) is a self-balancing binary search tree data structure. It's a variant of the binary search tree, designed to maintain a balance between its left and right subtrees. 

This balance ensures that the tree remains roughly balanced, which leads to efficient insertion, deletion, and search operations.

## Characteristics
In an AVL tree:
- Each node has two children: a left child (left subtree) and a right child (right subtree).
- The height of each subtree is **at most 1 more than the other**.
- This balance ensures that the tree's height remains relatively small, making search, insertion, and deletion operations efficient.

## Implementation
### C++
```c++
#include <iostream>
using namespace std;

// Define Node structure
struct Node {
    int key;
    Node* left, *right;

    // Constructor for creating a new node
    Node(int k) : key(k), left(nullptr), right(nullptr) {}
};

// AVL Tree class
class AVLTree {
public:
    Node* root;  // Root of the tree

    AVLTree() : root(nullptr) {}

    // Insert a node with given key
    void insertNode(int key);

    // Print the tree in inorder traversal
    void printInorder();

private:
    // Helper function to balance the tree after insertion or deletion
    Node* balance(Node* node);

    // Helper function to rotate right subtree
    Node* rightRotate(Node* node);

    // Helper function to rotate left subtree
    Node* leftRotate(Node* node);
};

// Implement insertion and balancing logic
void AVLTree::insertNode(int key) {
    Node* newNode = new Node(key);

    if (root == nullptr || root->key != key) {
        if (root == nullptr) {
            root = newNode;
        } else {
            Node* current = root;

            while (true) {
                if (newNode->key < current->key) {
                    if (current->left == nullptr) {
                        current->left = newNode;
                        break;
                    }
                    current = current->left;
                } else {
                    if (current->right == nullptr) {
                        current->right = newNode;
                        break;
                    }
                    current = current->right;
                }
            }

            // Balance the tree after insertion
            root = balance(root);
        }
    }
}

// Implement balancing logic for AVL Tree
Node* AVLTree::balance(Node* node) {
    int heightDiff = getHeight(node->left) - getHeight(node->right);

    if (heightDiff > 1) {  // Left-heavy subtree, need to balance right
        if (getHeight(node->left->left) >= getHeight(node->left->right)) {
            return rightRotate(node);
        } else {
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }
    }

    if (heightDiff < -1) {  // Right-heavy subtree, need to balance left
        if (getHeight(node->right->left) >= getHeight(node->right->right)) {
            return leftRotate(node);
        } else {
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }
    }

    return node;  // Tree is already balanced, no need to balance
}

// Helper function to get the height of a subtree
int AVLTree::getHeight(Node* node) {
    if (node == nullptr) {
        return 0;
    }
    return 1 + max(getHeight(node->left), getHeight(node->right));
}

// Implement rotation logic for AVL Tree
Node* AVLTree::rightRotate(Node* node) {
    Node* temp = node->left;
    node->left = temp->right;
    temp->right = node;

    return temp;
}

Node* AVLTree::leftRotate(Node* node) {
    Node* temp = node->right;
    node->right = temp->left;
    temp->left = node;

    return temp;
}

int main() {
    AVLTree tree;

    // Insert nodes with keys 5, 3, and 2
    tree.insertNode(5);
    tree.insertNode(3);
    tree.insertNode(2);

    // Print the inorder traversal of the AVL tree
    tree.printInorder();

    return 0;
}
```

This example demonstrates basic operations on an AVL tree:
- Insertion: The insertNode function inserts a new node with the given key. It also balances the tree after insertion to maintain its AVL properties.
- Balancing: The balance function checks if the tree is left-heavy or right-heavy and adjusts the tree by rotating nodes as needed.
- Rotation: The rightRotate and leftRotate functions perform rotations on the tree to balance it.

## Runtime Complexity
The runtime complexity of an AVL tree depends on the operations performed on the tree.
- **Search**: The search operation in an AVL tree has a runtime complexity of **O(log n)**, where n is the number of nodes in the tree. This is because the tree is self-balancing, ensuring that the height of the tree remains relatively small.
- **Insertion**: Inserting a node into an AVL tree also has a runtime complexity of **O(log n)**. The insertion operation involves updating the tree's structure to maintain its AVL properties, which takes logarithmic time.
- **Deletion**: Deleting a node from an AVL tree has a runtime complexity of **O(log n)** as well. The deletion operation involves adjusting the tree's structure to maintain its AVL properties, which also takes logarithmic time.
- **Traversal**: Traversing the tree (e.g., inorder, preorder, postorder) has a runtime complexity of **O(n)**, where n is the number of nodes in the tree.
