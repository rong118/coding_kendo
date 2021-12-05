# 82. Remove Duplicates from Sorted List II

## Question link
(https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

## Question Description
Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

<img src="https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg" width="400" />

Example 1:
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]

Example 2:
Input: head = [1,1,1,2,3]
Output: [2,3]

Constraints:
- The number of nodes in the list is in the range [0, 300].
- -100 <= Node.val <= 100
- The list is guaranteed to be sorted in ascending order.

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* dummy_node = new ListNode(INT_MAX, head);
        ListNode* pre = dummy_node;
        ListNode* cur = head;
        while(cur != NULL && cur->next != NULL){
            if(cur->val == cur->next->val){
                int v = cur->val;
                while(cur != NULL && cur->val == v){
                    cur = cur->next;
                }
                pre->next = cur;
            }else{
                pre = pre->next;
                cur = cur->next;
            }
        }
        return dummy_node->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)