# 716 Max Stack

## Question link
> (https://leetcode.com/problems/max-stack/)

## Question Description
Design a max stack that supports push, pop, top, peekMax and popMax.

push(x) -- Push element x onto stack.
pop() -- Remove the element on top of the stack and return it.
top() -- Get the element on the top.
peekMax() -- Retrieve the maximum element in the stack.
popMax() -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

Example 1:

> MaxStack stack = new MaxStack();
> stack.push(5); 
> stack.push(1);
> stack.push(5);
> stack.top(); -> 5
> stack.popMax(); -> 5
> stack.top(); -> 1
> stack.peekMax(); -> 5
> stack.pop(); -> 1
> stack.top(); -> 5

Note:
- -1e<sup>7</sup> <= x <= 1e<sup>7</sup>
- Number of operations won't exceed 10000.
- The last four operations won't be called when stack is empty.

## Tags
stack

## Code Implementation
```c++
class MaxStack {
public:
    /** initialize your data structure here. */
    MaxStack() {}
    
    void push(int x) {
        if (s2.empty() || s2.top() <= x) s2.push(x);
        s1.push(x);
    }
    
    int pop() {
        if (!s2.empty() && s2.top() == s1.top()) s2.pop();
        int t = s1.top(); s1.pop();
        return t;
    }
    
    int top() {
        return s1.top();
    }
    
    int peekMax() {
        return s2.top();
    }
    
    int popMax() {
        int mx = s2.top();
        stack<int> t;
        while (s1.top() != s2.top()) {
            t.push(s1.top()); s1.pop();
        }
        s1.pop(); s2.pop();
        while (!t.empty()) {
            push(t.top()); t.pop();
        }
        return mx;
    }

private:
    stack<int> s1, s2;
};
```

## Time Complexity Analysis
Running time  : O(n)