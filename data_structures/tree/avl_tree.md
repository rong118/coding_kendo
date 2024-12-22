# AVL Tree

An AVL tree (Adelson-Velskii and Landis) is a self-balancing binary search tree data structure. It's a variant of the binary search tree, designed to maintain a balance between its left and right subtrees. 

This balance ensures that the tree remains roughly balanced, which leads to efficient insertion, deletion, and search operations.

## Characteristics
In an AVL tree:
- Each node has two children: a left child (left subtree) and a right child (right subtree).
- The height of each subtree is **at most 1 more than the other**.
- This balance ensures that the tree's height remains relatively small, making search, insertion, and deletion operations efficient.

## Implementation
### Python
```python
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

class AVLTree:
    def __init__(self):
        self.root = None

    # Insert a node with the given key
    def insert_node(self, key):
        if self.root is None:
            self.root = Node(key)
        else:
            self.root = self._insert(self.root, key)

    # Recursive function to insert a node in the AVL Tree
    def _insert(self, node, key):
        if node is None:
            return Node(key)
        
        if key < node.key:
            node.left = self._insert(node.left, key)
        else:
            node.right = self._insert(node.right, key)

        # Balance the tree after insertion
        return self.balance(node)

    # Balance the AVL Tree and perform rotations if needed
    def balance(self, node):
        balance_factor = self.get_height(node.left) - self.get_height(node.right)

        # Left heavy
        if balance_factor > 1:
            if self.get_height(node.left.left) >= self.get_height(node.left.right):
                return self.right_rotate(node)
            else:
                node.left = self.left_rotate(node.left)
                return self.right_rotate(node)

        # Right heavy
        if balance_factor < -1:
            if self.get_height(node.right.right) >= self.get_height(node.right.left):
                return self.left_rotate(node)
            else:
                node.right = self.right_rotate(node.right)
                return self.left_rotate(node)

        return node  # No balancing needed

    # Perform a right rotation
    def right_rotate(self, y):
        x = y.left
        T2 = x.right

        # Perform rotation
        x.right = y
        y.left = T2

        return x

    # Perform a left rotation
    def left_rotate(self, x):
        y = x.right
        T2 = y.left

        # Perform rotation
        y.left = x
        x.right = T2

        return y

    # Get the height of a node
    def get_height(self, node):
        if node is None:
            return 0
        return 1 + max(self.get_height(node.left), self.get_height(node.right))

    # Print the tree using inorder traversal
    def print_inorder(self):
        self._inorder(self.root)

    # Helper function for inorder traversal
    def _inorder(self, node):
        if node:
            self._inorder(node.left)
            print(node.key, end=" ")
            self._inorder(node.right)


# Example usage
tree = AVLTree()

# Insert nodes with keys 5, 3, and 2
tree.insert_node(5)
tree.insert_node(3)
tree.insert_node(2)

# Print the inorder traversal of the AVL tree
tree.print_inorder()

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
