# 142. Linked List Cycle II

## Question link
(https://leetcode.com/problems/linked-list-cycle-ii/)

## Question Description
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.



Example 1:

![Image](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

> Input: head = [3,2,0,-4], pos = 1
>
> Output: tail connects to node index 1
>
> Explanation: There is a cycle in the linked list, where tail connects to the second node.

Example 2:

![Image](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

> Input: head = [1,2], pos = 0
>
> Output: tail connects to node index 0
>
> Explanation: There is a cycle in the linked list, where tail connects to the first node.

Example 3:

![Image](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

> Input: head = [1], pos = -1
> 
> Output: no cycle
>
> Explanation: There is no cycle in the linked list.

Constraints:
- The number of the nodes in the list is in the range [0, 10<sup>4</sup>].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>
- pos is -1 or a valid index in the linked-list.

## 分类 && 解题思路
- linkedlist

## Code Implementation
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        
        while(fast != NULL){
            slow = slow->next;
            fast = fast->next;
            if(fast != NULL) 
                fast = fast->next;
            else 
                return NULL;
            
            if(fast == slow){
                while(head != fast){
                    head = head->next;
                    fast = fast->next;
                }        
                return fast;
            }
        }

        return NULL;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)