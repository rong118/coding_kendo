# B-Tree

A B-tree is a self-balancing search tree data structure used in databases and file systems to efficiently store and retrieve large amounts of data. 

It's a variation of the binary search tree that's designed to minimize the number of disk I/O operations required when searching, inserting, or deleting nodes.

## Key characteristics:
- Each node can have multiple keys (values) and child nodes.
- The maximum number of children for each node is set by the **fanout factor** (e.g., 3-4).
- All keys in a node are stored in sorted order.
- Child nodes are stored in a contiguous block, making it easier to read and write data.

## Maintain Balance
A B-tree maintains balance by ensuring that:
- Each node has at most two children: This limits the maximum number of child nodes, which in turn helps maintain a balanced tree structure.
- The height of the tree is relatively constant: By ensuring each node has at most two children, the tree's height remains roughly the same even as data is inserted or deleted.
- To achieve this balance, B-trees use various techniques:
  - **Splitting nodes**: When a node becomes too full (i.e., it contains more than the fanout factor number of child nodes), it is split into two smaller nodes. This process maintains the balanced tree structure.
  - **Merging nodes**: When a node becomes too empty (i.e., it contains fewer than the minimum number of child nodes required by the fanout factor), it is merged with its sibling node to maintain the balanced tree structure.
  - **Rotating nodes**: During insertion or deletion, if a node becomes unbalanced (e.g., one side has many more children than the other), the B-tree can rotate nodes to rebalance the tree.
