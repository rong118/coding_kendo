# 83. Remove Duplicates from Sorted List

## Question link
(https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

## Question Description
Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

<img src="https://assets.leetcode.com/uploads/2021/01/04/list1.jpg" width="400" />

Example 1:
> Input: head = [1,1,2]
> Output: [1,2]

Example 2:
> Input: head = [1,1,2,3,3]
> Output: [1,2,3]

Constraints:
- The number of nodes in the list is in the range [0, 300].
- -100 <= Node.val <= 100
- The list is guaranteed to be sorted in ascending order.

## 分类 && 解题思路
-linkedlist

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* cur = head;
        while(cur != NULL){
            while(cur->next != NULL && cur->val == cur->next->val){
                ListNode* tmp = cur->next;
                cur->next = tmp->next;
                tmp->next = NULL;
            }
            cur = cur->next;
        }

        return head;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)