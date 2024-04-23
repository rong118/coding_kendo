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
