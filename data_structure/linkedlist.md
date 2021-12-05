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
- [160 Intersection of Two Linked Lists](../leetcode_questions/160_intersection_of_two_linked_lists.md)

4.删除
- [203 Remove Linked List Elements](../leetcode_questions/203_remove_linked_list_elements.md)
- [83 Remove Duplicates from Sorted List](../leetcode_questions/83_remove_duplicates_from_sorted_list.md)
- [82 Remove Duplicates from Sorted List II](../leetcode_questions/82_remove_duplicates_from_sorted_list_II.md)
- [19 Remove Nth Node From End of List](../leetcode_questions/19_remove_Nth_node_from_end_of_list.md)
- [1171 Remove Zero Sum Consecutive Nodes from Linked List](../leetcode_questions/1171_remove_zero_sum_consecutive_nodes_from_linkedlist.md)

5.复制
- [234 Palindrome Linked List](../leetcode_questions/234_palindrome_linked_list.md)
- [138 Copy List with Random Pointer](../leetcode_questions/138_copy_list_with_random_pointer.md)

6.结构转换
- [426 Convert Binary Search Tree to Sorted Doubly Linked List](../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md)