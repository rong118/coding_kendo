# 21. Merge Two Sorted Lists

## Question link
(https://leetcode.com/problems/merge-two-sorted-lists/)

## Question Description
Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.

<img src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" width="400"/>

Example 1:
> Input: l1 = [1,2,4], l2 = [1,3,4]
>
> Output: [1,1,2,3,4,4]

Example 2:
> Input: l1 = [], l2 = []
>
> Output: []

Example 3:
> Input: l1 = [], l2 = [0]
>
> Output: [0]

Constraints:
- The number of nodes in both lists is in the range [0, 50].
- -100 <= Node.val <= 100
- Both l1 and l2 are sorted in non-decreasing order.

## Tags
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* tail = dummy;
        
        while(l1 != NULL && l2 != NULL){
            ListNode* t;
            if(l1->val <= l2->val){
                t = l1;
                l1 = l1->next;
            }else{
                t = l2;
                l2 = l2->next;
            }
            
            tail->next = t;
            tail = t;
        }
        
        tail->next = (l1 != NULL) ? l1 : l2;
        
        return dummy->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)