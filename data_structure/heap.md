# PriorityQueue (Heap)
## 定义
堆分为两种:最大堆和最小堆，两者的差别在于节点的排序方式。
在最大堆中，父节点的值比每一个子节点的值都要大。 在最小堆中，父节点的值比每一个子节点的值都要小。 这就是所谓的“堆属性”，并且这个属性对堆中的每一个 节点都成立。

<img src="../assets/heap.png" width="300" />

```c++
std::priority_queue<int> pq;
pq.push(5);
pq.push(1);

int f = pq.top();  // 1
pq.pop();          // pop 1
```

## 应用
pq应用和array手动实现heap