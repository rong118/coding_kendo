# Stack

A Stack is a fundamental data structure that follows the Last-In-First-Out (LIFO) principle. It's a collection of elements where each element is added and removed from the top of the stack.

## Key Characteristics:
- Last-In-First-Out (LIFO): The last element added to the stack will be the first one to be removed.
- Top: The top element of the stack is the most recently added or removed element.
- Push: Adding an element to the stack, which moves the top element up one position.
- Pop: Removing the top element from the stack.

## Operations:
- Push (or Enqueue): Add an element to the top of the stack.
- Pop (or Dequeue): Remove the top element from the stack and return it.
- Peek: Return the top element without removing it from the stack.

## Implementation
### C++ Implementation by using std::stack
```c
// c++ Implementation
#include <stack>
#include <iostream>

int main() {
    std::stack<int> stack;

    stack.push(1);
    stack.push(2);
    stack.push(3);

    std::cout << "Peek: " << stack.top() << std::endl;

    int popped = stack.pop();
    std::cout << "Popped: " << popped << std::endl;

    return 0;
}
```

### Golang Implementation
```go
package main

import "fmt"

type Stack struct {
    array []int
    top   int
}

func (s *Stack) Push(element int) {
    if s.top >= len(s.array)-1 {
        fmt.Println("Stack is full!")
        return
    }
    s.array = append(s.array, element)
    s.top++
}

func (s *Stack) Pop() int {
    if s.top < 0 {
        fmt.Println("Stack is empty!")
        return -1 // or some other sentinel value
    }
    result := s.array[s.top]
    s.array = s.array[:s.top]
    s.top--
    return result
}

func (s *Stack) Peek() int {
    if s.top < 0 {
        fmt.Println("Stack is empty!")
        return -1 // or some other sentinel value
    }
    return s.array[s.top]
}

func main() {
    stack := &Stack{[]int{}, 0}
    stack.Push(1)
    stack.Push(2)
    stack.Push(3)

    fmt.Println("Peek:", stack.Peek())

    popped := stack.Pop()
    fmt.Println("Popped:", popped)
}
```

### Python Implementation
```python
# Stack Implementation Using List
stack = []

# Push Elements onto the Stack
stack.append(10)
stack.append(20)
stack.append(30)
print("Stack after pushing:", stack)  # Output: [10, 20, 30]

# Pop Elements from the Stack
print("Popped:", stack.pop())  # Output: 30
print("Stack after popping:", stack)  # Output: [10, 20]

# Peek at the Top Element
print("Top element:", stack[-1])  # Output: 20

# Check if the Stack is Empty
print("Is stack empty?", len(stack) == 0)  # Output: False
```

## Run Time Complexity:
- Push operation: O(1) (constant time)
- Pop operation: O(1) (constant time)
- Peek operation: O(1) (constant time)

## Leetcode Questions
- [155 Min Stack](../../leetcode_questions/23_merge_k_sorted_lists.md)
- [232 Implement Stack Using Queues](../../leetcode_questions/232_implement_stack_using_queues.md)
- [716 Max Stack](../../leetcode_questions/716_max_stack.md)
- [895 Maximum Frequency Stack](../../leetcode_questions/895_maximum_frequency_stack.md)
- [1381 Design a Stack With Increment Operation](../../leetcode_questions/1381_design_a_stack_with_increment_operation.md)
