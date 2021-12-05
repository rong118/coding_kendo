# 426. Convert Binary Search Tree to Sorted Doubly Linked List

## Question link
(https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/)

## Question Description
Convert a Binary Search Tree to a sorted Circular Doubly-Linked List in place.

You can think of the left and right pointers as synonymous to the predecessor and successor pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

We want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. You should return the pointer to the smallest element of the linked list.

Example 1:
> Input: root = [4,2,5,1,3]
>
> Output: [1,2,3,4,5]

Example 2:
> Input: root = [2,1,3]
>
> Output: [1,2,3]

Example 3:
> Input: root = []
>
> Output: []
>
> Explanation: Input is an empty tree. Output is also an empty Linked List.

Example 4:
> Input: root = [1]
>
> Output: [1]

## 分类 && 解题思路
- linkedlist
- tree

## Code Implementation
```c++
class Solution {
    Node* head = null;
    Node* pre = null;
public:
    Node* treeDoublylist(Node* root) {
        if(root == null) return root;
        inorderedTraversal(root);
        head->left = pre;
        pre->right = head;
    }

    void inorderedTraversal(Node* root){
        if(root == NULL) return;
        inorderedTraversal(root->left);
        if(head == NULL) head = root;
        if(pre != NULL){
            pre->right = root;
            root->left = pre;
        }
        pre = root;
        inorderedTraversal(root->right)
    }
};
```

## Time Complexity Analysis