# Stack
## 定义
栈是一种特殊的线性表，仅能在线性表的一端操 作，栈顶允许操作，栈底不允许操作。先进后出，或者说是后进先出，从栈顶放入元 素的操作叫入栈，取出元素叫出栈

<img src="../assets/stack.png" width="250" />

Last In First Out (LIFO) or First In Last Out (FILO)


```c++
// c++ Implementation
#include <stack>

stack<int> stk; // 常用method,时间复杂度均为O(1) 
stack.push(5)
stack.top()
stack.pop()
stack.isempty() //查看栈是否为空
```

## 应用
栈常应用于实现递归功能方面的场景，DFS均可以使用栈来实现

## Leetcode questions
- [155 Min Stack](../leetcode_questions/23_merge_k_sorted_lists.md)
- [232 Implement Stack Using Queues](../leetcode_questions/232_implement_stack_using_queues.md)
- [716 Max Stack](../leetcode_questions/716_max_stack.md)
- [1381 Design a Stack With Increment Operation](../leetcode_questions/1381_design_a_stack_with_increment_operation.md)
- [895 Maximum Frequency Stack](../leetcode_questions/895_maximum_frequency_stack.md)