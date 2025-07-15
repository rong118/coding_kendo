# 206. Reverse Linked List

## Question link
(https://leetcode.com/problems/reverse-linked-list/)

## Question Description
Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:
> Input: head = [1,2,3,4,5]
> Output: [5,4,3,2,1]

Example 2:
> Input: head = [1,2]
> Output: [2,1]

Example 3:
> Input: head = []
> Output: []

Constraints:
- The number of nodes in the list is the range [0, 5000].
- -5000 <= Node.val <= 5000

<b>Follow up</b>: A linked list can be reversed either iteratively or recursively. Could you implement both?

## Tags
- linkdelist

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
    ListNode* reverseList(ListNode* head) {
        ListNode* newHead = NULL;
        ListNode* cur = head;
        while(cur != NULL){
            ListNode* next = cur->next;
            cur->next = newHead;
            newHead = cur;
            cur = next;
        }

        return newHead;
    }
};

// Recursive
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        return reverse(head, NULL);
    }

    ListNode* reverse(ListNode* head, ListNode* newHead){
        if(head == NULL) return newHead;
        ListNode* next = head->next;
        head->next = newHead;
        newHead = head;
        return reverse(next, newHead);
    }
};
```

## Time Complexity Analysis
Running time  : O(n)