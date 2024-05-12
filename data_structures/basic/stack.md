# Stack

In computer science, a stack is an abstract data type that serves as a collection of elements, with two main operations:

Push, which adds an element to the collection, and
Pop, which removes the most recently added element that was not yet removed.

Additionally, a peek operation can, without modifying the stack, return the value of the last element added. Calling this structure a stack is by analogy to a set of physical items stacked one atop another, such as a stack of plates.

<img src="../assets/stack.png" width="300" />

## Implementation
```c
// c++ Implementation
#include <stack>
#include <iostream>

using namespace std;

int main(){
  stack<int> stk;           // 常用method,时间复杂度均为O(1) 
  stk.push(5);              // {5}
  stk.push(3);              // {3, 5}
  cout<<stk.top()<<endl;    // 3
  stk.pop();                // {5}
  cout<<stk.top()<<endl;    // 5
  stk.pop();                // {}
  stk.isempty();            // empty stack 

  return 0;
}
```

```go
// go Implementation with using gods
package main

import "github.com/emirpasic/gods/stacks/arraystack"

func main() {
	stack := arraystack.New() // empty
	stack.Push(1)             // 1
	stack.Push(2)             // 1, 2
	stack.Values()            // 2, 1 (LIFO order)
	_, _ = stack.Peek()       // 2,true
	_, _ = stack.Pop()        // 2, true
	_, _ = stack.Pop()        // 1, true
	_, _ = stack.Pop()        // nil, false (nothing to pop)
	stack.Push(1)             // 1
	stack.Clear()             // empty
	stack.Empty()             // true
	stack.Size()              // 0
}
```

## Features
* Last In First Out (LIFO) or First In Last Out (FILO)
* A stack is needed to implement depth-first search.

## Leetcode questions
- [155 Min Stack](../../leetcode_questions/23_merge_k_sorted_lists.md)
- [232 Implement Stack Using Queues](../../leetcode_questions/232_implement_stack_using_queues.md)
- [716 Max Stack](../../leetcode_questions/716_max_stack.md)
- [1381 Design a Stack With Increment Operation](../../leetcode_questions/1381_design_a_stack_with_increment_operation.md)
- [895 Maximum Frequency Stack](../../leetcode_questions/895_maximum_frequency_stack.md)
