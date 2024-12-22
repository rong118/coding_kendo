# Queue

A queue is a collection of entities that are maintained in a sequence with FIFO (First-In-First-Out) and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence. 
By convention, the end of the sequence at which elements are added is called the back, tail, or rear of the queue, and the end at which elements are removed is called the head or front of the queue, analogously to the words used when people line up to wait for goods or services.

## Queue's Characteristics:
- Enqueue (add): Add an element to the end of the queue.
- Dequeue (remove): Remove the front element from the queue.
- Front: The first element in the queue (the one that's been there the longest).
- Rear: The last element added to the queue.

## Implementation
### C++ Implementation using std::queue
```c
#include <iostream>
#include <queue>

int main() {
    std::queue<int> q;

    q.push(10);
    q.push(20);
    q.push(30);

    std::cout << q.front() << std::endl; // Output: 10
    q.pop();
    std::cout << q.front() << std::endl; // Output: 20
    q.pop();
    std::cout << q.front() << std::endl; // Output: 30
    q.pop();

    return 0;
}
```

### Golang Implementation using slices
```go
package main

import (
    "fmt"
)

type Queue struct {
    items []int
}

func (q *Queue) Enqueue(item int) {
    q.items = append(q.items, item)
}

func (q *Queue) Dequeue() int {
    if len(q.items) == 0 {
        return -1 // or any appropriate error handling
    }
    item := q.items[0]
    q.items = q.items[1:]
    return item
}

func main() {
    queue := Queue{}
    queue.Enqueue(10)
    queue.Enqueue(20)
    queue.Enqueue(30)

    fmt.Println(queue.Dequeue()) // Output: 10
    fmt.Println(queue.Dequeue()) // Output: 20
    fmt.Println(queue.Dequeue()) // Output: 30
}

```
### Python Example
```python
from collections import deque

# Create a Queue
queue = deque()

# Enqueue Elements
queue.append(10)
queue.append(20)
queue.append(30)
print("Queue after enqueuing:", queue)  # Output: deque([10, 20, 30])

# Dequeue Elements
print("Dequeued:", queue.popleft())  # Output: 10
print("Queue after dequeuing:", queue)  # Output: deque([20, 30])

# Peek at the Front Element
print("Front element:", queue[0])  # Output: 20

# Check if the Queue is Empty
print("Is queue empty?", len(queue) == 0)  # Output: False

```

## Runtime Complexity
- Enqueue (Addition):
  - Array-based implementation: O(1) average case, O(n) worst case if resizing is needed.
  - Linked list-based implementation: O(1) constant time.

- Dequeue (Removal):
  - Array-based implementation: O(1) constant time.
  - Linked list-based implementation: O(1) constant time.

- Peek (Access the Front Element):
  - Both array-based and linked list-based implementations: O(1) constant time.

- isEmpty (Check if the Queue is Empty):
  - Both array-based and linked list-based implementations: O(1) constant time.

# Deque (Double ended queue)

A deque, short for "double-ended queue," is a data structure that allows the insertion and deletion of elements from both the front and the back end. It combines the features of both stacks (Last-In-First-Out) and queues (First-In-First-Out).

## Implementation
### Python Implementation
```python
from collections import deque

# 1. Basic Operations
# Creating a Deque
dq = deque()  # Empty deque
dq = deque([10, 20, 30])  # Initialize with elements
print("Deque:", dq)  # Output: deque([10, 20, 30])

# Adding Elements
dq.append(40)  # Add to the right
dq.appendleft(5)  # Add to the left
print("After appending:", dq)  # Output: deque([5, 10, 20, 30, 40])

# Removing Elements
dq.pop()  # Remove from the right
print("After popping right:", dq)  # Output: deque([5, 10, 20, 30])
dq.popleft()  # Remove from the left
print("After popping left:", dq)  # Output: deque([10, 20, 30])

# 2. Iterating Through a Deque
# Forward Iteration
print("Forward iteration:", end=" ")
for item in dq:
    print(item, end=" ")  # Output: 10 20 30
print()

# Reverse Iteration
print("Reverse iteration:", end=" ")
for item in reversed(dq):
    print(item, end=" ")  # Output: 30 20 10
print()

# 3. Other Useful Methods
# Checking Length
print("Length of deque:", len(dq))  # Output: 3

# 4. Clearing the Deque
dq.clear()
print("After clearing:", dq)  # Output: deque([])

# 5. Rotating Elements
dq = deque([1, 2, 3, 4, 5])
dq.rotate(2)  # Rotate right by 2 positions
print("After rotating right:", dq)  # Output: deque([4, 5, 1, 2, 3])
dq.rotate(-1)  # Rotate left by 1 position
print("After rotating left:", dq)  # Output: deque([5, 1, 2, 3, 4])

# 6. Extending a Deque
dq = deque([1, 2])
dq.extend([3, 4, 5])  # Extend from the right
print("After extending right:", dq)  # Output: deque([1, 2, 3, 4, 5])
dq.extendleft([0, -1])  # Extend from the left
print("After extending left:", dq)  # Output: deque([-1, 0, 1, 2, 3, 4, 5])
```

## Leetcode Questions
- [225 Implement Stack using Queues](../../leetcode_questions/225_implement_stack_using_queue.md)
- [622 Design Circular Queue](../../leetcode_questions/622_design_circular_queue.md)
- [641 Design Circular Deque](../../leetcode_questions/641_design_circular_deque.md)
