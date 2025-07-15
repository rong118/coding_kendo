# 23. Merge k Sorted Lists

## Question link
> (https://leetcode.com/problems/merge-k-sorted-lists/)

## Question Description
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

Example 1:
> Input: lists = [[1,4,5],[1,3,4],[2,6]]
> Output: [1,1,2,3,4,4,5,6]
> Explanation: The linked-lists are:
> [
>  1->4->5,
>  1->3->4,
>  2->6
> ]
> merging them into one sorted list:
> 1->1->2->3->4->4->5->6

Example 2:
> Input: lists = []
> Output: []

Example 3:
> Input: lists = [[]]
> Output: []

Constraints:
- k == lists.length
- 0 <= k <= 10<sup>4</sup>
- 0 <= lists[i].length <= 500
- -10^<sup>4</sup> <= lists[i][j] <= 10^<sup>4</sup>
- lists[i] is sorted in ascending order.
- The sum of lists[i].length won't exceed 10^<sup>4</sup>.

## Tags
- heap
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

 // heap
class Solution {
public:
    struct compNode {
        bool operator()(ListNode *p, ListNode *q) const {
            return p->val>q->val;
        }  
    };

    ListNode *mergeKLists(vector<ListNode *> &lists) {
        priority_queue<ListNode*, vector<ListNode*>, compNode> pq;
        ListNode *dummy = new ListNode(0), *tail = dummy;
        
        for(int i=0; i<lists.size(); i++) 
            if(lists[i]) pq.push(lists[i]);
            
        while(!pq.empty()) {
            tail->next = pq.top();
            tail = tail->next;
            pq.pop();
            if(tail->next) pq.push(tail->next);
        }
        
        return dummy->next;
    }
};

// linkedlist O(nlogn)
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode *> &lists) {
       return partion(lists, 0, lists.size() - 1);
    }

    ListNode* partion(vector<ListNode *> &lists, int start, int end){
        if(start == end) return lists[start];
        if(start < end){
            int mid = (start + end)/2;
            ListNode* l1 = partion(lists, start, mid);
            ListNode* l2 = partion(lists, mid + 1, end);
            return merge(l1, l2);
        }
        return NULL;
    }

    ListNode* merge(ListNode* l1, ListNode* l2){
        if(l1 == NULL) return l2;
        if(l2 == NULL) return l1;
        if(l1->val < l2->val) {
            l1->next = merge(l1->next, l2);
            return l1;
        }else{
            l2->next = merge(l1, l2->next);
            return l2;
        }
    }
};
```

## Time Complexity Analysis
Running time  : O(nlog(n))