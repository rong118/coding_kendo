# 160. Intersection of Two Linked Lists

## Question link
(https://leetcode.com/problems/intersection-of-two-linked-lists/)

## Question Description
Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

For example, the following two linked lists begin to intersect at node c1:
<img src="https://assets.leetcode.com/uploads/2021/03/05/160_statement.png" width="400" />

The test cases are generated such that there are no cycles anywhere in the entire linked structure.
Note that the linked lists must retain their original structure after the function returns.

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2021/03/05/160_example_1_1.png" width="400" />
>
> Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
>
> Output: Intersected at '8'
>
> Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.

Example 2:

> <img src="https://assets.leetcode.com/uploads/2021/03/05/160_example_2.png" width="400" />
>
> Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
>
> Output: Intersected at '2'
>
> Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.

Example 3:

> <img src="https://assets.leetcode.com/uploads/2021/03/05/160_example_3.png" width="400" />
>
> Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
>
> Output: No intersection
>
> Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.

Constraints:
- The number of nodes of listA is in the m.
- The number of nodes of listB is in the n.
- 1 <= m, n <= 3 * 10<sup>4</sup> 
- 1 <= Node.val <= 10<sup>5</sup> 
- 0 <= skipA < m
- 0 <= skipB < n
- intersectVal is 0 if listA and listB do not intersect.
- intersectVal == listA[skipA] == listB[skipB] if listA and listB intersect.

Follow up: Could you write a solution that runs in O(m + n) time and use only O(1) memory?

注解：

a + c + b = a + b + c

<img src="../assets/abc.png" width="400" />

## Tags
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
 // see picture : a + c + b = a + b + c
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* a = headA;
        ListNode* b = headB;
        while(a != b){
            a = (a == NULL) ? headB : a->next;
            b = (b == NULL) ? headA : b->next;
        }

        return a;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)