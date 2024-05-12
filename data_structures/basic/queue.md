# Queue

A queue is a collection of entities that are maintained in a sequence and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence. By convention, the end of the sequence at which elements are added is called the back, tail, or rear of the queue, and the end at which elements are removed is called the head or front of the queue, analogously to the words used when people line up to wait for goods or services.

<img src="../assets/queue.png" width="350" />

## Implementation
```c
// c++ Implementation
#include <queue>
#include <iostream>

int main (){
  std::queue<int> q;                 // empty queue
  
  for(int i = 0; i < 5; i++){
    q.push(100 + i);
  }

  std::cout << q.front() << std::endl;
  std::cout << q.back() << std::endl;

  q.pop();

  return 0;
}
```

```go
// go Implementation with GoDs
package main

import llq "github.com/emirpasic/gods/queues/linkedlistqueue"

// LinkedListQueueExample to demonstrate basic usage of LinkedListQueue
func main() {
    q := llq.New()     // empty
    q.Enqueue(1)       // 1
    q.Enqueue(2)       // 1, 2
    _ = q.Values()     // 1, 2 (FIFO order)
    _, _ = q.Peek()    // 1,true
    _, _ = q.Dequeue() // 1, true
    _, _ = q.Dequeue() // 2, true
    _, _ = q.Dequeue() // nil, false (nothing to deque)
    q.Enqueue(1)       // 1
    q.Clear()          // empty
    q.Empty()          // true
    _ = q.Size()       // 0
}
```

## Features
* First In First Out (FIFO)
* A queue is needed to implement breath-first search.

## Leetcode questions
- [225 Implement Stack using Queues](../leetcode_questions/225_implement_stack_using_queue.md)
- [622 Design Circular Queue](../leetcode_questions/622_design_circular_queue.md)
- [641 Design Circular Deque](../leetcode_questions/641_design_circular_deque.md)


# Deque (Double ended queue)


In computer science, a double-ended queue (abbreviated to deque) is an abstract data type that generalizes a queue, for which elements can be added to or removed from either the front (head) or back (tail).

## Implementation

```c
// c++ Implementation
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

```go
// Go Implementation

```