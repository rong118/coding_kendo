# Deque (Double ended queue)

## 定义
如果把条件放松一下，允许两头都进，两头都出，这种队列叫双 端队列(Double Ended Queue)，学名Deque (deck)。

```c++
// c++ Implementation
#include <deque>

std::deque<int> q;
q.push_back(5);
q.push_front(1);
q.pop_back();
q.pop_front();
```