# 1650 Lowest Common Ancestor of a Binary Tree III

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/)

## Question Description
Given two nodes of a binary tree p and q, return their lowest common ancestor (LCA).
Each node will have a reference to its parent node. The definition for Node is below:
```
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
}
```

According to the definition of LCA on Wikipedia: "The lowest common ancestor of two nodes p and q in a tree T is the lowest node that has both p and q as descendants (where we allow a node to be a descendant of itself)."

Example 1:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
>
> Output: 3
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5 since a node can be a descendant of itself according to the LCA definition.

> Example 3:
> Input: root = [1,2], p = 1, q = 2
>
> Output: 1

Constraints:
- The number of nodes in the tree is in the range [2, 10<sup>5</sup>]
- -10^<sup>9</sup> <= Node.val <= 10^<sup>9</sup> 
- All Node.val are unique.
- p != q
- p and q exist in the tree.

## Tags
- tree
- linkedlist

## Code Implementation
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* parent;
};
*/

class Solution {
public:
    // space O(1) linkedlist 链表找交点
    Node* lowestCommonAncestor(Node* p, Node * q) {
        Node* a = p, *b = q;
        while (a != b) {
            a = (a == nullptr ? q : a->parent);
            b = (b == nullptr ? p : b->parent);
        }
        return a;
    }
};
```

## Time Complexity Analysis
