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
- Breadth First Search
- Depth First Search

## Leetcode questions
1. 遍历
- [144 Binary Tree Preorder Traversal](../leetcode_questions/144_binary_tree_preorder_traversal.md)
- [94 Binary Tree Inorder Traversal](../leetcode_questions/94_binary_tree_inorder_traversal.md)
- [145 Binary Tree Postorder Traversal](../leetcode_questions/145_binary_tree_postorder_traversal.md)
- [102 Binary Tree Level Order Traversal](../leetcode_questions/102_binary_tree_level_order_traversal.md)
- [103 Binary Tree Zigzig Level Order Traversal](../leetcode_questions/103_binary_tree_zigzig_level_order_traversal.md)
- [107 Binary Tree Level Order Traversal II](../leetcode_questions/107_binary_tree_level_order_traversal_II.md)
- [314 Binary Tree Vertical Order Traversal](../leetcode_questions/314_binary_tree_vertical_order_traversal.md)
- [987 Vertical Order Traversal of a Binary Tree](../leetcode_questions/987_vertical_order_traversal_of_a_binary_tree.md)

2. 结构转换/序列化
- [297 Serialize and Deserialize Binary Tree](../leetcode_questions/297_serialize_and_deserialize_binary_tree.md)
- [428 Serialize and Deserialize N-ary Tree](../leetcode_questions/428_serialize_and_deserialize_nary_tree.md)
- [449 Serialize and Deserialize BST](../leetcode_questions/449_serialize_and_deserialize_BST.md)
- [1008 Construct Binary Search Tree from Preorder Traversal](../leetcode_questions/1008_construct_binary_search_tree_from_preorder_traversal.md)
- [105 Construct Binary Tree from Preorder and Inorder Traversal](../leetcode_questions/105_construct_binary_tree_from_preorder_and_inorder_traversal.md)
- [106 Construct Binary Tree from Inorder and Postorder Traversal](../leetcode_questions/106_construct_binary_tree_from_inorder_and_postorder_traversal.md)
- [889 Construct Binary Tree from Preorder and Postorder Traversal](../leetcode_questions/889_construct_binary_tree_from_preorder_and_postorder_traversal.md)
- [426 Convert Binary Search Tree to Sorted Doubly Linked List](../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md)

3. Path (传递) => DFS (recursive)
- [257 Binary Tree Paths](../leetcode_questions/257_binary_tree_paths.md)
- [1448 Count Good Nodes in Binary Tree](../leetcode_questions/1448_count_good_nodes_in_binary_tree.md)
- [124 Binary Tree Maximum Path Sum](../leetcode_questions/124_binary_tree_maximum_path_sum.md)
- [1120 Maximum Average Subtree](../leetcode_questions/1120_maximum_average_subtree.md)
- [1372 Longest ZigZag Path in a Binary Tree](../leetcode_questions/1372_longest_zigzag_path_in_a_binary_tree.md)
- [1123 Lowest Common Ancestor of Deepest Leaves](../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md)
- [549 Binary Tree Longest Consecutive Sequence II](../leetcode_questions/549_binary_tree_longest_consecutive_sequence_ii.md)
