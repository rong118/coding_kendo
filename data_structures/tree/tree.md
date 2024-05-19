# Tree

Tree is a widely used abstract data type that represents a hierarchical structure with a set of connected nodes.
Each node in the tree can be connected to many children (depending on the type of tree), but must be connected to exactly one parent, except for the root node, which has no parent.
- No node can be its own ancestor (no loop).
- Each child can be treated like the root node of its own subtree.

## Types of Trees:
- Binary Tree: Each node has at most two child nodes (left and right).
- B-Tree: A self-balancing tree used in databases to manage disk storage.
- AVL Tree: A self-balancing binary search tree that ensures the height of the left and right subtrees differs by at most one.

## Balancing

In the context of trees, balancing refers to a process that maintains the structural properties of the tree while performing insertion or deletion operations. The goal is to keep the tree approximately balanced, so that search, insertion, and deletion operations remain efficient (typically O(log n) in the average case).

## Tree Runtime Complexity
- Search: O(log n), where n is the number of nodes in the tree. This is because trees can be searched efficiently using algorithms like binary search.
- Insertion: O(log n) to O(n), depending on the type of tree and the insertion algorithm used. For example, inserting a node into a balanced binary search tree takes O(log n) time, while inserting a node into an unbalanced tree can take O(n) time.
- Deletion: O(log n) to O(n), depending on the type of tree and the deletion algorithm used.
- Traversal: O(n), where n is the number of nodes in the tree. This is because traversing a tree involves visiting each node, which takes constant time per node.

## Tree's Traversal
- Preorder  (root-left-right)
- Inorder   (left-root-right) 
- Postorder (let-right-root)

## Search on the Tree
- Breadth First Search (BFS)
- Depth First Search (DFS)
