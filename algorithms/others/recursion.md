# Recursion

A recursive algorithm is a method of solving a problem where the solution involves solving smaller instances of the same problem. Recursive algorithms typically have a base case (or cases) that end the recursion and one or more recursive cases that divide the problem into smaller subproblems.

## Key Characterist
- Base Case:
    The condition under which the recursion ends. This is usually a simple case that can be solved directly without further recursion.
- Recursive Case: 
    The part of the algorithm where the function calls itself with a smaller or simpler input.

## Example 1: Factorial Function

The factorial of a non-negative integer n (denoted as n!) is the product of all positive integers less than or equal to n.

### Python Implementation
```python
def factorial(n):
    # Base case: factorial of 0 or 1 is 1
    if n == 0 or n == 1:
        return 1
    # Recursive case: n! = n * (n-1)!
    else:
        return n * factorial(n - 1)
```

### Runtime Complexity

The time complexity of a recursive algorithm depends on:
1. The number of recursive calls made.
2. The work done outside of the recursive calls.

The time complexity of the factorial function is O(n), because there are n recursive calls, each doing a constant amount of work.

## Example 2: Fibonacci Sequence

The Fibonacci sequence is defined as:

- F(0) = 0
- F(1) = 1
- F(n) = F(n − 1) + F(n − 2) for n > 1

### Python Implementation
```python
def fibonacci(n):
    # Base cases
    if n == 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

### Runtime Complexity

The naive recursive implementation of Fibonacci has exponential time complexity, O(2^n), because it recomputes values multiple times.

## Improving Recursive Algorithms

Recursive algorithms can sometimes be optimized using techniques such as:

- **Memoization**
    Storing the results of expensive function calls and reusing them when the same inputs occur again.
- **Dynamic Programming** 
    Breaking the problem into simpler subproblems and solving them just once, storing their solutions.

### Improved Fibonacci Sequence

This reduces the time complexity to O(n) as each number's fibonacci only caculate one time

```python
def fibonacci(n, memo={}):
    # Base cases
    if n == 0:
        return 0
    elif n == 1:
        return 1
    # Check if value is already computed
    if n in memo:
        return memo[n]
    # Compute and store the value
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]
```