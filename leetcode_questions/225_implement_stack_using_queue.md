# 225. Implement Stack using Queues

## Question link
(https://leetcode.com/problems/implement-stack-using-queues/)

## Question Description
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:
- void push(int x) Pushes element x to the top of the stack.
- int pop() Removes the element on the top of the stack and returns it.
- int top() Returns the element on the top of the stack.
- boolean empty() Returns true if the stack is empty, false otherwise.

Notes:
- You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.

Example 1:

> Input
> ["MyStack", "push", "push", "top", "pop", "empty"]
> [[], [1], [2], [], [], []]
> Output
> [null, null, null, 2, 2, false]
>
> Explanation
> MyStack myStack = new MyStack();
> myStack.push(1);
> myStack.push(2);
> myStack.top(); // return 2
> myStack.pop(); // return 2
> myStack.empty(); // return False

Constraints:
- 1 <= x <= 9
- At most 100 calls will be made to push, pop, top, and empty.
- All the calls to pop and top are valid.
 
## Tags
- queue

## Code Implementation
```c++
class MyStack {
private:
    queue<int> que1;
    queue<int> que2;
public:
    MyStack() {}
    
    // Push element x onto stack.
    void push(int x) {
        que1.push(x);
    }

    // Removes the element on top of the stack.
    int pop() {
        while(que1.size() > 1){
            int tmp = que1.front();
            que1.pop();
            que2.push(tmp);
        }
        int ans = que1.front();
        que1.pop();
        
        while(que2.size() != 0){
            int tmp = que2.front();
            que2.pop();
            que1.push(tmp);
        }
        return ans;
    }

    // Get the top element.
    int top() {
        int res;
        while(que1.size()!=0){
            if(que1.size()==1)
                res=que1.front();
            int tmp=que1.front();
            que1.pop();
            que2.push(tmp);
        }
        
        while(que2.size()!=0){
            int tmp=que2.front();
            que2.pop();
            que1.push(tmp);
        }
        
        return res;
    }

    // Return whether the stack is empty.
    bool empty() {
        return que1.size()==0 && que2.size()==0;
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

## Time Complexity Analysis