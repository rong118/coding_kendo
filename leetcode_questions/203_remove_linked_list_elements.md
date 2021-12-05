# 203. Remove Linked List Elements

## Question link
(https://leetcode.com/problems/remove-linked-list-elements/)

## Question Description
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

<img src="https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg" width="400" />

Example 1:
> Input: head = [1,2,6,3,4,5,6], val = 6
> 
> Output: [1,2,3,4,5]

Example 2:
> Input: head = [], val = 1
>
> Output: []

Example 3:
> Input: head = [7,7,7,7], val = 7
>
> Output: []

Constraints:
- The number of nodes in the list is in the range [0, 10<sup>4</sup> ].
- 1 <= Node.val <= 50
- 0 <= val <= 50

## 分类 && 解题思路
- linkedlit

## Code Implementation
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */

 // Iterative
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0, head);
        ListNode* cur = dummy;

        while(cur->next != NULL ){
            if(cur->next->val == val){
                cur->next = cur->next->next;
            }else{
                cur = cur->next;
            }
        }

        return dummy->next;
    }
};

// Recursive
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(head == NULL) return NULL;
        head->next = removeElements(head->next, val);
        return head->val == val ? head->next : head;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)