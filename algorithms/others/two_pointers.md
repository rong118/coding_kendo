# Two Pointers

The two pointers algorithm is a commonly used technique in computer science and competitive programming, particularly for solving problems related to arrays and linked lists. 

The idea is to use two pointers to iterate through the data structure, typically starting at different positions.

## How It Works
- **Initialization**: Two pointers are initialized at different positions.
- **Movement**: The pointers move towards each other (or specific rules) until they meet or satisfy a certain condition.
- **Condition Checking**: At each step, the algorithm checks a condition involving the elements at the pointers' positions.

### Pseudocode
```
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. left++
            2. right--
            3. Both left++ and right--
```

## Examples

### Finding Pair with Given Sum in a Sorted Array
```python
def find_pair_with_sum(arr, target_sum):
    left = 0
    right = len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target_sum:
            return (arr[left], arr[right])
        elif current_sum < target_sum:
            left += 1
        else:
            right -= 1
    
    return None

# Example usage
arr = [1, 2, 3, 4, 6]
target_sum = 6
print(find_pair_with_sum(arr, target_sum))  # Output: (2, 4)
```

## Runtime Efficiency 
The two pointers algorithm often leads to efficient solutions with a time complexity of O(n) or O(nlogn) depending on the problem, which is usually better than brute force approaches.