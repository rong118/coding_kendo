# 234. Palindrome Linked List

## Question link
(https://leetcode.com/problems/palindrome-linked-list/)

## Question Description
Given the head of a singly linked list, return true if it is a palindrome.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" width="400" />
>
> - Input: head = [1,2,2,1]
>
> - Output: true

Example 2:
> - Input: head = [1,2]
>
> - Output: false
 
Constraints:
- The number of nodes in the list is in the range [1, 105].
- 0 <= Node.val <= 9

Follow up: Could you do it in O(n) time and O(1) space?

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
    bool isPalindrome(ListNode* head) {
        ListNode* FirstHalfEnd = _endOfFirstHalf(head);
        ListNode* secondHalfStart = _reverse(FirstHalfEnd->next);
        ListNode* p1 = head;
        ListNode* p2 = secondHalfStart;
        bool result = true;
        while(result && p2 != NULL){
            if(p1->val != p2->val) result = false;
            p1 = p1->next;
            p2 = p2->next;
        }
        FirstHalfEnd->next = _reverse(secondHalfStart);
        return result;
    }

    ListNode* _endOfFirstHalf(ListNode* head){
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast->next != NULL && fast->next->next != NULL){
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;
    }

    ListNode* _reverse(ListNode* head){
        ListNode* prev = NULL;
        while(head != NULL){
            ListNode* next = head->next;
            head->next = prev;
            prev = head;
            head = next;
        }

        return prev;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)