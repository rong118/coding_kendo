# Sliding Window

The "sliding window" algorithm is a technique used to solve problems that involve finding subarrays (or subsequences) within a larger array or string. 

It operates by maintaining a window of elements within the array and sliding this window across the entire array to find a solution efficiently.

## Basic Steps:
- **Initialize Pointers**:

        Define two pointers (usually left and right) to represent the current window or subarray.

- **Expand the Window**:

        Expand the window by moving the right pointer to the right to include more elements. Check if the current window satisfies the conditions or constraints given in the problem.

        If the window satisfies the condition, attempt to minimize it by moving the left pointer to the right, thus contracting the window.

- **Track the Optimal Solution**:

        While expanding and contracting the window, keep track of the optimal solution found that meets the problem's requirements.

- **Repeat Until the End**:

        Continue this process until the right pointer has traversed the entire array or string.

## Example

### Find the maximum sum of a subarray of length k in an array
```python
def max_sum_subarray(arr, k):
    n = len(arr)
    if k > n:
        return "Invalid input"
    
    max_sum = float('-inf')
    current_sum = sum(arr[:k])
    
    for i in range(n - k + 1):
        if current_sum > max_sum:
            max_sum = current_sum
        if i + k < n:
            current_sum = current_sum - arr[i] + arr[i + k]
    
    return max_sum

# Example usage:
arr = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
print("Maximum sum of a subarray of length", k, ":", max_sum_subarray(arr, k))
```

## Runtime Effiency

The sliding window algorithm is generally linear in time complexity O(n), making it efficient for many array and string processing problems where to find an optimal subarray or substring.