# Array

Array is a fundamental data structure that stores elements of the same data type in contiguous memory locations, allowing efficient random access to its elements by index.

## Implementation
### Python Example
```python
numbers = [10, 20, 30, 40, 50]
print(numbers[0], numbers[-1])  # Access
numbers[2] = 35                 # Modify
for num in numbers: print(num) # Iterate

numbers = [3, 6, 1, 8, 2]
numbers.sort(); print(numbers)     # [1, 2, 3, 6, 8]
numbers.reverse(); print(numbers) # [8, 6, 3, 2, 1]
print(max(numbers), min(numbers), sum(numbers))
```

## Runtime Complexity
- **Access**: O(1)
- **Insert/Delete**: O(n) (O(1) at end)

## Dynamic Array

A **dynamic array** (or resizable/growable array) supports **runtime resizing** while retaining key features like **random access** and **contiguous memory**.

Unlike static arrays, it adjusts size automatically when capacity is exceeded by allocating more memory and copying existing elements.

## Implementation
### Python Example using List:
```python
dynamic_array = []
dynamic_array.append(1)
dynamic_array.append(2)
dynamic_array.append(3)
dynamic_array.remove(2)

print(len(dynamic_array))  # 2
print(" ".join(map(str, dynamic_array)))
```

## Leetcode Questions
- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [15. Three Sum](../../leetcode_questions/15_three_sum.md)
- [26. Remove Duplicates From Sorted Array](../../leetcode_questions/26_remove_duplicates_from_sorted_array.md)
- [27. Remove Element](../../leetcode_questions/27_remove_element.md)
- [75. Sort Colors](../../leetcode_questions/75_sort_colors.md)
- [169. Majority Element](../../leetcode_questions/169_majority_element.md)
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
- [238. Product of Array Except Self](../../leetcode_questions/238_product_of_array_except_self.md)