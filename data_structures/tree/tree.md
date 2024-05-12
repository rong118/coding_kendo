# Tree


<img src="../assets/tree.png" width="300" />

Tree is a widely used abstract data type that represents a hierarchical structure with a set of connected nodes.
Each node in the tree can be connected to many children (depending on the type of tree), but must be connected to exactly one parent, except for the root node, which has no parent.
No node can be its own ancestor (no loop).
Each child can be treated like the root node of its own subtree.


## Binary Tree
Binary trees are a commonly used type, which constrain the number of children for each parent to exactly two.

<img src="../assets/binarytree.svg.png" width="300" />

```c
// c++ Implementation
class TreeNode {
public:
    TreeNode* left;
    TreeNode* right;
    
    int val;
    TreeNode(int n){
        val = n;
        left = NULL;
        right = NULL;
    }
}

int main(){
  TreeNode* root = new TreeNode(0); 
  root->left  = new TreeNode(1); 
  root->right = new TreeNode(2);
  
  std::cout<< root->val << std::endl;
  std::cout<< root->left->val << std::endl;
  return 0;
}
```

## Perfect Binary Tree /  Full Binary Tree / Complete Binary Tree

<img src="../assets/perfectBinaryTree.png" width="600" />

## Balanced Binary Tree
左右两个子树的高度绝对值布超过1， 并且左右两个子树都是一个平衡树， 平衡二叉树必定是平衡搜索树。
- AVL tree
- red-black tree
- B, B-, B+ tree

## 树的遍历
- preorder  (根左右)
- inorder   (左根右) 
- postorder (左右根)

<img src="../assets/treetraversal.png" width="400" />
<img src="../assets/treeTraversalResult.png" width="400" />


```c
// c++ Implementation
// Resusive
vector<int> treeTraversal(TreeNode* root){
    vector<int> ans;
    helper(root, ans);
    return ans;
}

// preorder
void helper(TreeNode* root, vector<int>& ans){
    if(root == NULL) return;
    ans.push_back(root->val);
    helper(root->left, ans);
    helper(root->right, ans);
}

// inorder
void helper(TreeNode* root, vector<int>& ans){
    if(root == NULL) return;
    helper(root->left, ans);
    ans.push_back(root->val);
    helper(root->right, ans);
}

// postorder
void helper(TreeNode* root, vector<int>& ans){
    if(root == NULL) return;
    helper(root->left, ans);
    helper(root->right, ans);
    ans.push_back(root->val);
}
```

## LCA Problem
Given a binary tree, find the lowest common ancestor of two (or more) given nodes in tree.
- 倍增、Tarjan、树链剖分 (TODO)


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

4. LCA
- [235 Lowest Common Ancestor of a Binary Search Tree](../leetcode_questions/235_lowest_common_ancestor_of_a_binary_search_tree.md)
- [236 Lowest Common Ancestor of a Binary Tree](../leetcode_questions/236_lowest_common_ancestor_of_a_binary_tree.md)
- [1644 Lowest Common Ancestor of a Binary Tree II](../leetcode_questions/1644_lowest_common_ancestor_of_a_binary_tree_ii.md)
- [1650 Lowest Common Ancestor of a Binary Tree III](../leetcode_questions/1650_lowest_common_ancestor_of_a_binary_tree_iii.md)
- [1676 Lowest Common Ancestor of a Binary Tree IV](../leetcode_questions/1676_lowest_common_ancestor_of_a_binary_tree_iv.md)
- [1123 Lowest Common Ancestor of Deepest Leaves](../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md)
- [865 Smallest Subtree with all the Deepest Nodes](../leetcode_questions/865_smallest_subtree_with_all_the_deepest_nodes.md)

4. Path (传递) => DFS (recursive)
- [257 Binary Tree Paths](../leetcode_questions/257_binary_tree_paths.md)
- [1448 Count Good Nodes in Binary Tree](../leetcode_questions/1448_count_good_nodes_in_binary_tree.md)
- [124 Binary Tree Maximum Path Sum](../leetcode_questions/124_binary_tree_maximum_path_sum.md)
- [1120 Maximum Average Subtree](../leetcode_questions/1120_maximum_average_subtree.md)
- [1372 Longest ZigZag Path in a Binary Tree](../leetcode_questions/1372_longest_zigzag_path_in_a_binary_tree.md)
- [1123 Lowest Common Ancestor of Deepest Leaves](../leetcode_questions/1123_lowest_common_ancestor_of_deepest_leaves.md)
- [549 Binary Tree Longest Consecutive Sequence II](../leetcode_questions/549_binary_tree_longest_consecutive_sequence_ii.md)
