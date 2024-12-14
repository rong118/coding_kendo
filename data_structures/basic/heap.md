# Heap

A heap is a specialized tree-based data structure that satisfies the following properties:
- Complete: The heap is either a full binary tree or a complete binary tree.
- Ordered: The elements in the heap are ordered according to a certain criterion, such as maximum or minimum values.

## Characteristics

- Parent-child relationships: Each node has at most two children (left and right).
- Heap property: The parent node is either greater than both child nodes (in a max-heap) or less than both child nodes (in a min-heap).

## Binary Heap

(Binary) Heap is a special case of balanced binary tree data structure where the root-node key is compared with its children and arranged accordingly.
Min-Heap − Where the value of the root node is less than or equal to either of its children.
Max-Heap − Where the value of the root node is greater than or equal to either of its children.

## Implementation

Heaps can be implemented using various data structures, such as:
- Arrays: Heaps can be represented using arrays, where the heap property is maintained by swapping elements.
- Linked lists: Heaps can also be implemented using linked lists, where each node has a parent-child relationship.
- Trees: Heaps can be viewed as a special type of tree, where the root node represents the maximum or minimum value.

## Heapify
HEAPIFY is an important process for manipulating heaps. Ensuring that it remains a valid heap. It's an essential step in various algorithms, such as heapsort and priority queue operations.

Its inputs are an array A and an index i into the array. When HEAPIFY is called, it is assumed that the binary trees rooted at LEFT(i) and RIGHT(i) are heaps, but that A[i] may be smaller than its children, thus violating the heap property. The function of HEAPIFY is to let the value at A[i] "float down" in the heap so that the subtree rooted at index i becomes a heap.

For example, given an integer array, heapify it into min-heap array
For a heap array A, A[0] is the root of heap, and for each A[i], A[i * 2 + 1] is the left child and A[j * 2 + 2] is the right child of A[i].

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

        //Once the condition is met, exits loop
        if(i == largest){
            break;
        }

        swap(arr, i, largest);
        i = largest;
    }
}
```

### HeapSort
```c++
void heap_sort(vector<int>& arr){
    int len = arr.size();

    // Build heap
    for(int i = len/2; i >= 0; i--){
        heapify(arr, len, i);
    }

    // One by one extract from heap
    for(int i = len - 1; i > 0 ;i--){
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heapify(arr, i, 0);
    }
}
```

## Runtime Complexity
- Insertion (Enqueue): **O(log n)**<br> 
  Inserting an element into a binary heap involves adding it to the end of the heap (maintaining the heap shape property) and then performing a "heapify up" operation to restore the heap property, which takes O(log n) time.

- Deletion (Dequeue): **O(log n)**<br> 
  Removing the root element (highest priority element in a max heap or lowest priority element in a min-heap) involves replacing it with the last element in the heap, then performing a "heapify down" operation to restore the heap property, which takes O(log n) time.

- Peeking: **O(1)**<br> 
    Accessing the root element of the heap (highest priority element) takes constant time, as it's always the first element in the underlying array representation of the heap.

- Building a Heap from an Array (Heapify): **O(n)**<br>
  Converting an array of elements into a heap (heapify operation) can be done in linear time complexity by starting from the last non-leaf node and performing a "heapify down" operation for each node. Since there are n/2 nodes in a binary heap, where n is the number of elements, building the heap takes O(n) time. T(n) =  O(n/4) + O(n/8 * 2) + O(n/16 * 3) ...
     =  O(n)

- Heap Sort: **O(n log n)**<br>
  Sorting elements using heap sort involves building a max heap from the array (O(n)), then repeatedly removing the root element and restoring the heap property (O(log n) per removal), resulting in a time complexity of O(n log n) for the entire sorting process.

# Priority Queue
Priority Queue (also known as Ordered Queue or Sorted Queue) is a data structure that allows you to insert elements with associated priorities, and then retrieve the element with the highest or lowest priority.

Operations:
- offer() => add element in queue
- pull()  => get and remove top element from queue
- peek()  => return top element

## Implementation
### C++ Implementation with heap
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

### C++ stl::queue
```c++
#include <queue>
#include <iostream>

int main() {
    // Create a max-heap priority queue (highest priority first)
    std::priority_queue<int, std::vector<int>, std::greater<int>> pq;

    // Insert some elements with priorities
    pq.push(3);
    pq.push(1);
    pq.push(5);
    pq.push(2);

    // Retrieve the highest-priority element (max-heap property)
    while (!pq.empty()) {
        std::cout << "Priority: " << pq.top() << std::endl;
        pq.pop();
    }

    return 0;
}
```

### Golang Implementation
```golang
package main

import "fmt"

type PQElement struct {
    value int
    prio  int // priority
}

func (e *PQElement) Less(other *PQElement) bool {
    return e.prio < other.prio
}

func main() {
    // Create a new priority queue
    pq := []PQElement{}

    // Enqueue some elements with priorities
    pq = append(pq, PQElement{value: 1, prio: 3})
    pq = append(pq, PQElement{value: 2, prio: 2})
    pq = append(pq, PQElement{value: 3, prio: 1})

    // Dequeue and print the highest-priority element
    for len(pq) > 0 {
        fmt.Println("Highest priority:", pq[0].value)
        pq = pq[1:]
    }
}
```

### Python: Using queue.PriorityQueue
```python
# Using queue.PriorityQueue
from queue import PriorityQueue

# Create a Priority Queue
pq = PriorityQueue()

# Enqueue elements with priorities
pq.put((2, "Task 2"))  # Priority 2
pq.put((1, "Task 1"))  # Priority 1
pq.put((3, "Task 3"))  # Priority 3

# Dequeue elements
while not pq.empty():
    print(pq.get())

```

# Python: Using queue.PriorityQueue with Custom Comparison
```python
class Task:
    def __init__(self, priority, deadline, description):
        self.priority = priority  # Lower values mean higher priority
        self.deadline = deadline  # Lower values mean earlier deadline
        self.description = description
    
    def __lt__(self, other):
        # Custom comparison: first by priority, then by deadline
        if self.priority == other.priority:
            return self.deadline < other.deadline  # earlier deadline gets higher priority
        return self.priority < other.priority  # lower priority number means higher priority
    
    def __repr__(self):
        return f"Task({self.priority}, {self.deadline}, '{self.description}')"

# Create a list of tasks
tasks = [
    Task(3, 5, "Write report"),
    Task(1, 2, "Fix critical bug"),
    Task(2, 3, "Review pull requests"),
    Task(1, 1, "Meet with manager"),  # Same priority as Task(1, 2), but earlier deadline
]

# Create a Priority Queue (min-heap)
pq = PriorityQueue()

# Enqueue tasks into the priority queue
for task in tasks:
    pq.put(task)

# Process tasks in order of priority and deadline
while not pq.empty():
    task = pq.get()  # Get the highest priority task (lowest priority number)
    print(f"Processing: {task.description} (Priority: {task.priority}, Deadline: {task.deadline})")

```

## Leetcode Questions
- [23 Merge k Sorted Lists](../../leetcode_questions/23_merge_k_sorted_lists.md)
- [347 Top K Frequent Elements](../../leetcode_questions/347_top_k_frequent_elements.md)
- [912 Sort_an_array](../../leetcode_questions/912_sort_an_array.md)
- [215 Kth_Largest_Element_in_an_Array](../../leetcode_questions/215_Kth_Largest_Element_in_an_Array.md)