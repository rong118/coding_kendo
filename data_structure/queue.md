# Queue
## 定义
队列与栈一样，也是一种线性表，不同的是，队列可以在 一端添加元素，在另一端取出元素，也就是:先进先出。

<img src="../assets/queue.png" width="350" />

First In First Out (FIFO)

```c++
// c++ Implementation
#include <stack>

std::queue<int> q;
q.push(5);
q.pop();
int f = q.front();
```

##
常用来实现BFS 宽度优先搜索的遍历