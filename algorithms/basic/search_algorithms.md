# Search Algorithm

A search algorithm is a technique used to find a specific element, pattern, or solution within a larger dataset, such as an array, list, tree, or graph. The goal of a search algorithm is to efficiently locate the desired item without having to examine every single element in the dataset.

There are many types of search algorithms, including:

- **Linear Search**: Finds an element by checking each element in order until it finds the target.

- **Binary Search**: Divides the search space in half with each iteration, reducing the number of comparisons needed to find the target.

- **Hash Table Search**: Uses a hash function to map keys to indices in an array, allowing for fast lookup and insertion operations.

- **Graph Traversal**: Visits nodes in a graph according to a set of rules or heuristics to find a specific node or pattern.

## I. Linear Search

Linear search is a simple and straightforward search algorithm that iterates through each element in the dataset until it finds the target. It works by:

### Linear Search Example
```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Found! Return the index.
    return -1  # Not found!

if __name__ == "__main__":
    arr = [2, 3, 4, 10, 40]
    target = 10

    result = linear_search(arr, target)

    if result != -1:
        print(f"Element found at index {result}")
    else:
        print("Element not found!")
```

### Runtime Complexity

Linear search has a time complexity of **O(n)**, where n is the size of the dataset.

## II. Binary Search

Binary search is a fast and efficient search algorithm used to find an element in a sorted array or list. It's based on the principle of repeatedly dividing the search space in half until you find the target element.

### Binary Search Example
```python
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid  # Found!
        elif arr[mid] < target:
            low = mid + 1  # Target is in the right half
        else:
            high = mid - 1  # Target is in the left half

    return -1  # Not found!

if __name__ == "__main__":
    arr = [2, 3, 4, 10, 40]
    target = 10

    result = binary_search(arr, target)

    if result != -1:
        print(f"Element found at index {result}")
    else:
        print("Element not found!")
```

### Runtime Complexity

The time complexity of binary search is **O(log n)**, where n is the size of the array. This means that as the size of the array grows, the running time of binary search increases logarithmically.

### Binary Search vs. Linear Search

**Advantages**: Binary search is much faster than linear search for large datasets since it only needs to examine half the elements in each iteration. It's also easy to implement and works well with sorted arrays.

**Disadvantages**: Binary search requires the array to be sorted, which may not always be the case. Additionally, if the target element is not present in the array, binary search will terminate without finding it (since it only checks elements within the range).
