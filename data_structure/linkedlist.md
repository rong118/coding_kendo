# Linked List
## 定义
链表是非连续，非顺序储存结构， 每个node包含数据和指针两部分
<img src="../assets/linkedlist.png" width="600" />

```c++
// c++ Implementation
struct {
    Node* ptr;
    int val;
} Node;

Node * ptr = new Node(1);
ptr->next = new Node(2);
int v = ptr->val;
```
赋值取值时间复杂度O(1)

优点：
- 可以随意添加减元素。
- 添加删除元素只需要改变前后节点指针

缺点
- 占用空间大
- 查找需要遍历

## 适用场景
需要频繁增加删除， 删除操作的场景

## Leetcode question
1.反转
- [206 Reverse Linked List](../leetcode_questions/206_reverse_linked_list.md)
- [92 Reverse Linked List II](../leetcode_questions/92_reverse_linked_list_II.md)
- [25 Reverse Nodes in K-Group](../leetcode_questions/25_reverse_nodes_in_k_group.md)

2.合并
- [2 Add Two Numbers](../leetcode_questions/2_add_two_numbers.md)
- [445 Add Two Numbers II](../leetcode_questions/445_add_two_numbers_II.md)
- [21 Merge Two Sorted Lists](../leetcode_questions/21_merge_two_sorted_lists.md)
- [23 Merge k sorted Lists](../leetcode_questions/23_merge_k_sorted_lists.md)

3.找环
- [141 Linked List Cycle](../leetcode_questions/141_linked_list_cycle.md)
- [142 Linked List Cycle II](../leetcode_questions/142_linked_list_cycle.md)
- [287 Find the Duplicate Number](../leetcode_questions/287_find_the_duplicate_number.md)

4.删除

5.复制

6.结构转换