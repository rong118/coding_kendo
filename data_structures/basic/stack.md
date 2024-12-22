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
