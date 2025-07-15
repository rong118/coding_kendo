# 445. Add Two Numbers II

## Question link
(https://leetcode.com/problems/add-two-numbers-ii/)

## Question Description
You are given two non-empty linked lists representing two non-negative integers. 
The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.


Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/04/09/sumii-linked-list.jpg" width="400" />
> Input: l1 = [7,2,4,3], l2 = [5,6,4]
>
> Output: [7,8,0,7]

Example 2:
> Input: l1 = [2,4,3], l2 = [5,6,4]
>
> Output: [8,0,7]

Example 3:
> Input: l1 = [0], l2 = [0]
>
> Output: [0]

Constraints:
- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* r1 = _reverseList(l1);
        ListNode* r2 = _reverseList(l2);
        ListNode* r = _addTwoNumbers(r1, r2);
        return _reverseList(r);
    }

    ListNode* _addTwoNumbers(ListNode *l1, ListNode *l2) {
        ListNode* head = new ListNode(0);  //output header
        ListNode* ptr = head;
        int carry = 0;
        int sum = 0;
        while(l1 != NULL || l2 != NULL || carry){   //a and b exist
            sum = (l1? l1->val : 0) + (l2 ? l2->val : 0) + carry;
            carry = sum / 10;
            sum = sum % 10;
            ptr->val = sum;
            ListNode* temp =new ListNode(0);
            
            l1 = l1 ? l1->next : l1;
            l2 = l2 ? l2->next : l2;
            
            if(l1 != NULL || l2 != NULL || carry){
                ptr->next = temp;
                ptr = ptr->next;
            }
        }

        return head;
    }

    ListNode* _reverseList(ListNode* l){
        ListNode* head = new ListNode(INT_MAX);
        ListNode* ptr = l;
        
        while(ptr != NULL){
            ListNode* tmp = ptr;
            ptr = ptr->next;
            ListNode* n = head->next;
            head->next = tmp;
            tmp->next = n;
        }
        
        return head->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)