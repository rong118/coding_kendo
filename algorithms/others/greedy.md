# Greedy Algorithm

A greedy algorithm is a problem-solving strategy that makes the locally optimal choice at each stage with the hope of finding a global optimum. 

It makes a series of decisions by selecting the best option available at the moment, without reconsidering previous decisions, aiming for a quick and efficient solution.

## Example: Jump Game

Given an array of non-negative integers, you are initially positioned at the first index. Each element in the array represents the maximum jump length from that position. 

Determine the minimum number of jumps required to reach the last index.

### Greedy Approach:

The greedy strategy for this problem involves iterating through the array and making decisions at each step to maximize the reach (furthest point) we can achieve with each jump.

### Implementation
```python
def jump(nums):
    n = len(nums)
    if n == 1:
        return 0
    
    jumps = 0
    current_end = 0
    furthest = 0
    
    for i in range(n - 1):
        furthest = max(furthest, i + nums[i])
        
        if i == current_end:
            jumps += 1
            current_end = furthest
            
            if current_end >= n - 1:
                break
    
    return jumps

# Example usage:
nums = [2, 3, 1, 1, 4]
print("Minimum number of jumps:", jump(nums))  # Output: 2
```

### Run-time Complexity

It operates in linear time O(n), where n is the length of the array, making it suitable for large inputs