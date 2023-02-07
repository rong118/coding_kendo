## Binary Search Tree :
- Binary Tree
- 左子树和右子树是有顺序的 
- 查找元素时间复杂度：lg(N)

<img src="../assets/bst.png" width="150" />

- BST 性质

<img src="../assets/bst_attribute.png" width="1200" />

- BST 查找
```c
// recursive
TreeNode* search(TreeNode* root, int target){
    if(root == NULL || root->val == target) return root;
    if(root->val < target) return search(root->right, target);

    return search(root->left, target);
}

// iterative
TreeNode* search(TreeNode* root, int target){
    TreeNode* cur = root;

    while(true){
        if(cur == NULL) return NULL;
        if(cur->val == target) return cur;
        if(cur->val < target) cur = cur->left;
        else cur = cur->right;
    }
    
    return NULL;
}
```

- BST 添加
```c
// recursive
TreeNode* insert(TreeNode* root, int target){
    if(root == NULL){
        root = new TreeNode(target);
        return root;
    }

    if(target < root->val) root->left = insert(root->left, target);
    else if(target > root->val) root->right = insert(root->right, target);

    return root;
}

// iterative
TreeNode* insert(TreeNode* root, int target){
    TreeNode* cur = root;
    TreeNode* newNode = new TreeNode(target);
    if(cur == NULL){
        cur = newNode;
        return cur;
    }

    TreeNode* prev = NULL;
    while(cur != NULL){
        prev = cur;
        if(cur->val < target) cur = cur.right;
        else cur = cur->left;
    }

    if(prev->val < target) prev->right = newNode;
    else prev->left = newNode;

    return root;
}

```

- BST 删减
=> leetcode 450


3. BST
- [270 Closest Binary Search Tree Value](../leetcode_questions/270_closest_binary_search_tree_value.md)
- [450 Delete Node in BST](../leetcode_questions/450_delete_node_in_BST.md)
- [98 Validate Binary Search Tree](../leetcode_questions/98_validate_binary_search_tree.md)
- [173 Binary Search Tree Iterator](../leetcode_questions/173_binary_search_tree_iterator.md)
- [99 Recover Binary Search Tree](../leetcode_questions/99_recover_binary_search_tree.md)
- [108 Convert Sorted Array to Binary Search Tree](../leetcode_questions/108_convert_sorted_array_to_binary_search_tree.md)
- [1382 Balance a Binary Search Tree](../leetcode_questions/1382_balance_a_binary_search_tree.md)
- [96 Unique Binary Search Trees](../leetcode_questions/96_unique_binary_search_trees.md)
- [95 Unique Binary Search Trees II](../leetcode_questions/95_unique_binary_search_trees_ii.md)

