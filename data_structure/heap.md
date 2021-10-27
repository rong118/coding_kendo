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

## Heapify
HEAPIFY is an important subroutine for manipulating heaps. Its inputs are an array A and an index i into the array. When HEAPIFY is called, it is assumed that the binary trees rooted at LEFT(i) and RIGHT(i) are heaps, but that A[i] may be smaller than its children, thus violating the heap property (7.1). The function of HEAPIFY is to let the value at A[i] "float down" in the heap so that the subtree rooted at index i becomes a heap.

For example, given an integer array, heapify it into min-heap array
For a heap array A, A[0] is the root of heap, and for each A[i], A[i *2 + 1] is the left child and A[j* 2 + 2] is the right child of A[i].

``` c++
void buildheap(vector<int>& arr){
    for(int i = arr.size()/2; i >= 0; i--){
        heapify(arr, arr.size(); i);
    }
}

// Heapify, root is node i
void heapify(vector<int> arr, int n, int i){
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;

    // If left child is larger than root
    if(l < n && arr[l] > arr[largest]){
        largest = l;
    }

    // If right child is larger than root
    if(r < n && arr[r] > arr[largest]){
        largest = r;
    }

    // If largest is not root
    if(largest != i){
        int swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;

        heapify(arr, n, largest);
    }
}

// Iterative 
void iterativeHeapify (vector<int>& arr, int i) {
    while(true){
        int l = 2 * i + 1;
        int r = 2 * i + 2;
        int largest = i;

        if(l < arr.size() && arr[l] > arr[largest]){
            largest = l;
        }

        if(r < arr.size() && arr[r] > arr[largest]){
            largest = r;
        }

        //Once condition is met, exit loop
        if(i == largest){
            break;
        }

        swap(arr, i, largest);
        i = largest;
    }
}
```

## Heapify Run Time
T(n) =  O(n/4) + O(n/8 * 2) + O(n/16 * 3) ...
     =  O(n)

## HeapSort
```c++
void heap_sort(vector<int>& arr){
    int len = arr.size();

    // Build heap
    for(int i = n/2; i >= 0; i--){
        heapify(arr, n, i);
    }

    // One by one extract from heap
    for(int i = n - 1; i > 0 ;i--){
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
    }

    heapify(arr, i, 0);
}
```

## Priority Queue
Method:
offer() => add element in queue
pull()  => get and remove top element from queue
peek()  => return top element

```c++
class priority_queue {
public:
    vector<int> queue;
    int pq_size;

    priority_queue(int n){
        this->queue.resize(n);
    }

    bool offer(int num){
        queue[pq_size] = num;
        siftUp(pq_size);
        pq_size++
        return true;
    }

    int poll() {
        int v = queue[0];
        queue[0] = queue[pq_size - 1];
        pq_size--;
        if(pq_size > 0) siftDown();
        return 
    }

    int peek() {
        if(pq_size == 0) return INT_MIN;
        return queue[0];
    }

private:
    void siftdown(int nodeIndex) {
        int smllest = nodeIndex;
        int left = 2 * nodeIndex + 1;
        int right = 2 * nodeIndex + 2;
        if (left < pq_size && queue[left] < queue[smallest]){
            smallest = left;
        }

        if (right < pq_size && queue[right] < queue[smallest]){
            smallest = right;
        }

        if(smallest != nodeIndex){
            swap(nodeIndex, smallest);
            siftDown(smallest);
        }
    }

    void siftUp(int nodeIndex) {
        if(nodeIndex != 0){
            int parentIndex = (nodeIndex - 1) / 2;
            if(queue[parentIndex] > queue[nodeIndex]){
                swap(parentIndex, nodeIndex);
            }
        }
    }

    void swap(int i, int j){
        int tmp = queue[i];
        queue[i] = queue[j];
        queue[j] = tmp;
    }
}
```

## Heap time complexity
peekMax() or peekMin(): depends on which heap you implement, takes O(1)
add()/remove(): a new number to heap would do logn times heapify, so time complexity is O(logn)
Delete random would cause O(n), because search O(n) + delete O(logn)
Build heap only takes O(n), we are doing heapify only for half of the element

## Leetcode questions