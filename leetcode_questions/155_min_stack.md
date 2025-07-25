# 155 Min Stack

## Question link
> (https://leetcode.com/problems/min-stack/)

## Question Description
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.

Example 1:
> Input
> ["MinStack","push","push","push","getMin","pop","top","getMin"]
> [[],[-2],[0],[-3],[],[],[],[]]
>
> Output
> [null,null,null,null,-3,null,0,-2]
>
> Explanation
> MinStack minStack = new MinStack();
> minStack.push(-2);
> minStack.push(0);
> minStack.push(-3);
> minStack.getMin(); // return -3
> minStack.pop();
> minStack.top();    // return 0
> minStack.getMin(); // return -2

Constraints:
- -2<sup>31</sup> <= val <= 2<sup>31</sup> - 1
- Methods pop, top and getMin operations will always be called on non-empty stacks.
- At most 3 * 10<sup>4</sup> calls will be made to push, pop, top, and getMin.

## Tags
- stack

## Code Implementation
```c++
class MinStack {
private:
    stack<int> mStk;   //keep input number
    stack<int> mMinStk; //trace minium number for each input;

public:
    void push(int x) {
        mStk.push(x);
        if(mMinStk.empty() || x <= mMinStk.top()){
            mMinStk.push(x);
        }
    }

    void pop() {
        if(mStk.top() <= mMinStk.top()){
            mMinStk.pop();
        }
        mStk.pop();
    }

    int top() {
        return mStk.top();
    }

    int getMin() {
        return mMinStk.top();
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
