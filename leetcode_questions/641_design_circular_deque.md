# 641. Design Circular Deque

## Question link
(https://leetcode.com/problems/design-circular-deque/)

## Question Description
Design your implementation of the circular double-ended queue (deque).

Implement the MyCircularDeque class:

- MyCircularDeque(int k) Initializes the deque with a maximum size of k.
- boolean insertFront() Adds an item at the front of Deque. Returns true if the operation is successful, or false otherwise.
- boolean insertLast() Adds an item at the rear of Deque. Returns true if the operation is successful, or false otherwise.
- boolean deleteFront() Deletes an item from the front of Deque. Returns true if the operation is successful, or false otherwise.
- boolean deleteLast() Deletes an item from the rear of Deque. Returns true if the operation is successful, or false otherwise.
- int getFront() Returns the front item from the Deque. Returns -1 if the deque is empty.
- int getRear() Returns the last item from Deque. Returns -1 if the deque is empty.
- boolean isEmpty() Returns true if the deque is empty, or false otherwise.
- boolean isFull() Returns true if the deque is full, or false otherwise.

Example
> Input
> ["MyCircularDeque", "insertLast", "insertLast", "insertFront", "insertFront", "getRear", "isFull", "deleteLast", "insertFront", "getFront"]
> [[3], [1], [2], [3], [4], [], [], [], [4], []]
> Output
> [null, true, true, true, false, 2, true, true, true, 4]
> 
> Explanation
> MyCircularDeque myCircularDeque = new MyCircularDeque(3);
> myCircularDeque.insertLast(1);  // return True
> myCircularDeque.insertLast(2);  // return True
> myCircularDeque.insertFront(3); // return True
> myCircularDeque.insertFront(4); // return False, the queue is full.
> myCircularDeque.getRear();      // return 2
> myCircularDeque.isFull();       // return True
> myCircularDeque.deleteLast();   // return True
> myCircularDeque.insertFront(4); // return True
> myCircularDeque.getFront();     // return 4

Constraints:
- 1 <= k <= 1000
- 0 <= value <= 1000
- At most 2000 calls will be made to insertFront, insertLast, deleteFront, deleteLast, getFront, getRear, isEmpty, isFull.

## Tags
- queue
- array point

## Code Implementation
```c++
class MyCircularDeque {
public:
    vector<int> q;
    int front, rear, size;
    MyCircularDeque(int k) {
        q.resize(k);
        front = 0;
        rear = -1;
        size = 0;
    }
    
    bool insertFront(int value) {
        if(!isFull()){
            if(--front < 0) front += q.size();
            q[front] = value;
            size++;
            if(size == 1) {rear = front};
            return true;
        }
        return false;
    }
    
    bool insertLast(int value) {
        if(!isFull()){
            rear = (rear + 1) % q.size();
            q[rear] = value;
            size++;
            return true;
        }

        return false;
    }
    
    bool deleteFront() {
        if(!isEmpty()){
            front = (front + 1) % q.size();
            size--;
            return true;
        }
        return false;
    }
    
    bool deleteLast() {
        if(!isEmpty()){
            if(--rear < 0) rear += q.size();
            size--;
            return true;
        }

        return false;
    }
    
    int getFront() {
        return isEmpty() ? -1 : q[front];
    }
    
    int getRear() {
        return isEmpty() ? -1 : q[rear];
    }
    
    bool isEmpty() {
        return size == 0;
    }
    
    bool isFull() {
        return size == q.size();
    }
};

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque* obj = new MyCircularDeque(k);
 * bool param_1 = obj->insertFront(value);
 * bool param_2 = obj->insertLast(value);
 * bool param_3 = obj->deleteFront();
 * bool param_4 = obj->deleteLast();
 * int param_5 = obj->getFront();
 * int param_6 = obj->getRear();
 * bool param_7 = obj->isEmpty();
 * bool param_8 = obj->isFull();
 */
```

## Time Complexity Analysis