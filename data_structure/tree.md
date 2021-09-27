# Tree

## 定义
树是一种数据结构:
每个节点有零个或多个子节点; 没有父节点的节点称为根节点;
每一个非根节点有且只有一个父节点; 
除了根节点外，每个子节点可以分为多个不相交的子树;

Binary Tree二叉树是树的特殊一种，具 有如下特点:
- 每个结点最多有两颗子树

<img src="../assets/binarytree.png" width="300" />

Binary Search Tree :
- Binary Tree
- 左子树和右子树是有顺序的 
- 查找元素时间复杂度：lg(N)

<img src="../assets/bst.png" width="150" />

```c++
// c++ Implementation
TreeNode* root = new TreeNode(0); 
root->left  = new TreeNode(1); 
root->right = new TreeNode(2);
```

## Balance