# 19. Remove Nth Node From End of List

## Question link
(https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## Question Description
Given the head of a linked list, remove the nth node from the end of the list and return its head.

<img src="" width="400" />

Example 1:
> Input: head = [1,2,3,4,5], n = 2
> Output: [1,2,3,5]

Example 2:
> Input: head = [1], n = 1
> Output: []

Example 3:
> Input: head = [1,2], n = 1
> Output: [1]

Constraints:
- The number of nodes in the list is sz.
- 1 <= sz <= 30
- 0 <= Node.val <= 100
- 1 <= n <= sz
 
## 分类 && 解题思路
- linkedlist

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
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(INT_MAX, head);
        ListNode* first = dummy;
        ListNode* second = dummy;
        while(n >= 0){
            second = second->next;
            n--;
        }
        
        while(second != NULL){
            first = first->next;
            second = second->next;
        }

        first->next = first->next->next;
        return dummy->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)