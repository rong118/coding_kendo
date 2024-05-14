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

### Javascript Implementation
```javascript
class Queue {
    constructor() {
        this.items = [];
    }

    enqueue(item) {
        this.items.push(item);
    }

    dequeue() {
        if (this.items.length === 0) {
            return -1; // or any appropriate error handling
        }
        return this.items.shift();
    }
}

const queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);

console.log(queue.dequeue()); // Output: 10
console.log(queue.dequeue()); // Output: 20
console.log(queue.dequeue()); // Output: 30
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
### C++ Implementation using std::deque
```c++
#include <deque>
#include <iostream>

int main (){
  std::deque<int> dq;                 // empty queue
  
  for(int i = 0; i < 5; i++){         // push back
    dq.push_back(100 + i);
  }

  for(int i = 0; i < 5; i++){         // push front
    dq.push_front(200 + i);
  }

  std::cout << q.front() << std::endl;
  std::cout << q.back() << std::endl;

  q.pop_front();
  q.pop_back();

  return 0;
}
```

### Golang Implementation
```go
package main

import "fmt"

type Deque struct {
    items []int
}

func (d *Deque) PushFront(item int) {
    d.items = append([]int{item}, d.items...)
}

func (d *Deque) PushBack(item int) {
    d.items = append(d.items, item)
}

func (d *Deque) PopFront() int {
    if len(d.items) == 0 {
        return -1 // or any appropriate error handling
    }
    item := d.items[0]
    d.items = d.items[1:]
    return item
}

func (d *Deque) PopBack() int {
    if len(d.items) == 0 {
        return -1 // or any appropriate error handling
    }
    item := d.items[len(d.items)-1]
    d.items = d.items[:len(d.items)-1]
    return item
}

func main() {
    deque := Deque{}
    deque.PushBack(10)
    deque.PushBack(20)
    deque.PushFront(5)

    fmt.Println(deque.PopFront()) // Output: 5
    fmt.Println(deque.PopBack())  // Output: 20
    fmt.Println(deque.PopFront()) // Output: 10
}
```

### Javascript Implementation
```javascript
class Deque {
    constructor() {
        this.items = [];
    }

    pushFront(item) {
        this.items.unshift(item);
    }

    pushBack(item) {
        this.items.push(item);
    }

    popFront() {
        if (this.isEmpty()) {
            return -1; // or any appropriate error handling
        }
        return this.items.shift();
    }

    popBack() {
        if (this.isEmpty()) {
            return -1; // or any appropriate error handling
        }
        return this.items.pop();
    }

    isEmpty() {
        return this.items.length === 0;
    }

    size() {
        return this.items.length;
    }

    peekFront() {
        return this.items[0];
    }

    peekBack() {
        return this.items[this.items.length - 1];
    }
}

// Example usage:
const deque = new Deque();
deque.pushBack(10);
deque.pushBack(20);
deque.pushFront(5);

console.log(deque.popFront()); // Output: 5
console.log(deque.popBack());  // Output: 20
console.log(deque.popFront()); // Output: 10
```

## Leetcode questions
- [225 Implement Stack using Queues](../../leetcode_questions/225_implement_stack_using_queue.md)
- [622 Design Circular Queue](../../leetcode_questions/622_design_circular_queue.md)
- [641 Design Circular Deque](../../leetcode_questions/641_design_circular_deque.md)
