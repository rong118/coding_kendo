# 92. Reverse Linked List II

## Question link
(https://leetcode.com/problems/reverse-linked-list-ii)

## Question Description
Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.

Example1

<img src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" width="400" />

> Input: head = [1,2,3,4,5], left = 2, right = 4
>
> Output: [1,4,3,2,5]

Example 2:
> Input: head = [5], left = 1, right = 1
>
> Output: [5]

Constraints:
- The number of nodes in the list is n.
- 1 <= n <= 500
- -500 <= Node.val <= 500
- 1 <= left <= right <= n

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
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* dummyHead = new ListNode(INT_MAX, head);
        ListNode* cur = dummyHead->next;
        ListNode* pre = dummyHead;
        int i = 1;
        while(cur != NULL && i < left){
            pre = cur;
            cur = cur->next;
            i++;
        }
        ListNode* last = pre;
        while(cur != NULL && i <= right){
            ListNode* next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
            i++;
        }

        ListNode* n = last->next;
        n->next = cur;
        last->next = pre;

        return dummyHead->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)