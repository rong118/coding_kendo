# PriorityQueue (Heap)
## 定义
堆分为两种:最大堆和最小堆，两者的差别在于节点的排序方式。
在最大堆中，父节点的值比每一个子节点的值都要大。 在最小堆中，父节点的值比每一个子节点的值都要小。 这就是所谓的“堆属性”，并且这个属性对堆中的每一个 节点都成立。

(Binary) Heap is a special case of balanced binary tree data structure where the root-node key is compared with its children and arranged accordingly.
Min-Heap − Where the value of the root node is less than or equal to either of its children.
Max-Heap − Where the value of the root node is greater than or equal to either of its children.


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