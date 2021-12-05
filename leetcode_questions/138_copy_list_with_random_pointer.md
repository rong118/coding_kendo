# 138. Copy List with Random Pointer

## Question link
(https://leetcode.com/problems/copy-list-with-random-pointer/)

## Question Description
A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes X and Y in the original list, where X.random --> Y, then for the corresponding two nodes x and y in the copied list, x.random --> y.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

- val: an integer representing Node.val
- random_index: the index of the node (range from 0 to n-1) that the random pointer points to, or null if it does not point to any node.

Your code will only be given the head of the original linked list.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2019/12/18/e1.png" width="400" />
>
> Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
>
> Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]

Example 2:
> <img src="https://assets.leetcode.com/uploads/2019/12/18/e2.png" width="400" />
>
> Input: head = [[1,1],[2,1]]
>
> Output: [[1,1],[2,1]]

Example 3:
> <img src="https://assets.leetcode.com/uploads/2019/12/18/e3.png" width="400" />
>
> Input: head = [[3,null],[3,0],[3,null]]
>
> Output: [[3,null],[3,0],[3,null]]

Example 4:
> Input: head = []
>
> Output: []
>
> Explanation: The given linked list is empty (null pointer), so return null.


Constraints:
- 0 <= n <= 1000
- -10000 <= Node.val <= 10000
- Node.random is null or is pointing to some node in the linked list.

## 分类 && 解题思路
- linkedlist

## Code Implementation
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

// hashmap running space : O(n)
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> m; // origial : copy

        // build map
        for(Node* cur = head; cur != NULL; cur = cur->next){
            m[cur] = new Node(cur->val);
        }

        // connection
        for(Node* cur = head; cur != NULL; cur = cur->next){
            m[cur]->next   = m[cur->next];
            m[cur]->random = m[cur->random];
        }

        return m[head];
    }
};

// linkedlist running space : O(1)
class Solution {
public:
    Node* copyRandomList(Node* head) {
        Node* cur = head;

        // insert each copy nodes after original
        while(cur != NULL){
            Node* copy = new Node(cur->val);
            Node* next = cur->next;
            cur->next = copy;
            copy->next = next;
            cur = next;
        }

        // connect random
        cur = head;
        while(cur != NULL){
            cur->next->random = cur->random ?  cur->random->next : NULL;
            cur = cur->next->next;
        }

        // separate to two lists
        cur = head;
        Node* retHead = new Node(INT_MAX);
        Node* retTail = retHead;
        while(cur != NULL){
            Node* next = cur->next;
            cur->next = next->next;
            cur = cur->next;
            retTail->next = next;
            retTail = retTail->next;
        }

        return retHead->next;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
