# Sorting Algortihms

Sorting algorithms are procedures that take an unsorted collection (or array) as input and produce a sorted collection as output. The goal is to arrange the elements in a specific order.

## Types of Sorting Algorithms

There are many sorting algorithms, each with its strengths and weaknesses. Some common types include:

- **Comparison-Based Sorting**: These algorithms compare elements to determine their order. Examples: **Bubble Sort**, **Selection Sort**, **Insertion Sort**, **Merge Sort**
- **Non-Comparison-Based Sorting**: These algorithms don't rely on comparisons. Examples: **QuickSort**, **Radix Sort**, **Counting Sort**
- **Hybrid Sorting**: Combines multiple sorting techniques. Examples: Timsort (used in Java), Introsort (used in C++)

## I. Bubble Sort

Bubble Sort is a simple, comparison-based sorting algorithm that repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

### Implementation
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]  # Swap elements
                swapped = True
        if not swapped:
            break  # Early exit if the list is already sorted

if __name__ == "__main__":
    arr = [4, 2, 7, 1, 3]
    bubble_sort(arr)
    print(" ".join(map(str, arr)))
```

### Runtime Complexity of Bubble Sort:
The runtime complexity of Bubble Sort is **O(n^2)**, where n is the number of elements in the input array.

## II. Selection Sort

Selection sort is a simple, comparison-based sorting algorithm that repeatedly finds the minimum element from unsorted part and puts it at the beginning. The input list is divided into two parts: sorted part and unsorted part.

### Implementation
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        # Find the minimum element in the unsorted part
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        # Swap found minimum with the first element of the unsorted part
        arr[i], arr[min_index] = arr[min_index], arr[i]

if __name__ == "__main__":
    arr = [5, 2, 8, 3, 1]

    print("Original array:", " ".join(map(str, arr)))

    selection_sort(arr)

    print("Sorted array:", " ".join(map(str, arr)))
```

### Runtime Complexity of Selection Sort
Selection Sort has a runtime complexity of O(n^2), where n is the number of elements in the input array.

## III. Merge Sort

Merge sort is a sorting algorithm that combines two sorted arrays into a single, sorted array. It's a **stable** sorting algorithm, which means it maintains the relative order of equal elements.

### Implementation
```python
def merge(arr, left, mid, right):
    # Create temporary arrays for the two halves
    n1 = mid - left + 1
    n2 = right - mid

    L = arr[left:left + n1]
    R = arr[mid + 1:mid + 1 + n2]

    # Initialize indices for the two halves
    i = 0
    j = 0
    k = left

    # Merge two halves into one array
    while i < n1 and j < n2:
        if L[i] <= R[j]:
            arr[k] = L[i]
            i += 1
        else:
            arr[k] = R[j]
            j += 1
        k += 1

    # Copy remaining elements from left half, if any
    while i < n1:
        arr[k] = L[i]
        i += 1
        k += 1

    # Copy remaining elements from right half, if any
    while j < n2:
        arr[k] = R[j]
        j += 1
        k += 1

def merge_sort(arr, left, right):
    if left < right:
        # Find the middle point of the array
        mid = (left + right) // 2

        # Recursively sort the two halves
        merge_sort(arr, left, mid)
        merge_sort(arr, mid + 1, right)

        # Merge the sorted halves
        merge(arr, left, mid, right)

def print_array(arr):
    print(" ".join(map(str, arr)))

# Main function to test the Merge Sort algorithm
if __name__ == "__main__":
    arr = [64, 34, 25, 12, 22, 11, 90]

    print("Original array:", end=" ")
    print_array(arr)

    merge_sort(arr, 0, len(arr) - 1)

    print("Sorted array:", end=" ")
    print_array(arr)
```

### Runtime Complexity

Merge sort has a time complexity of **O(nlogn)**, where n is the length of the input array. The space complexity is O(n), as we need to store the temporary arrays during the merging process.

## IV. Quick Sort

Quick sort is a high efficient sorting algorithm developed by Tony Hoare in 1962. It is an in-place sorting algorithm, which means it doesn't require any extra space to store the elements being sorted.

The key idea behind Quicksort is that it uses the pivot element as a "divider" to split the array into two smaller arrays: one with elements less than the pivot and another with elements greater than the pivot. This partitioning step makes it possible to sort the entire array using only a few recursive calls.

### Implementation
```python
def swap(a, b):
    return b, a

def partition(arr, low, high):
    pivot = arr[high]  # Choose the last element as the pivot
    i = low - 1  # Index of smaller element

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = swap(arr[i], arr[j])

    arr[i + 1], arr[high] = swap(arr[i + 1], arr[high])  # Move pivot to its correct position
    return i + 1

def quicksort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)  # Partition the array and get the pivot index

        # Recursively sort subarrays on either side of the pivot
        quicksort(arr, low, pi - 1)
        quicksort(arr, pi + 1, high)

def print_array(arr):
    print(" ".join(map(str, arr)))

if __name__ == "__main__":
    arr = [64, 34, 25, 12, 22, 11, 90]

    print("Original array:", end=" ")
    print_array(arr)

    quicksort(arr, 0, len(arr) - 1)

    print("Sorted array:", end=" ")
    print_array(arr)
```

### Runtime Complexity

The runtime complexity of Quicksort depends on the pivot selection and partitioning scheme used:

- Average-Case Time Complexity: **O(n log n)** - This is the most common case where the pivot element is chosen in a way that the partitioning step takes linear time.
- Best-Case Time Complexity: **O(n)** - This occurs when the pivot element is the median of the array, and all elements are either less than or greater than the pivot. In this case, the partitioning step can be done in constant time.
- Worst-Case Time Complexity: **O(n^2)** - This occurs when the pivot element is chosen poorly, such as being the smallest or largest element in the array. In this case, one of the recursive calls will have a very small input size (n/2), leading to an exponential increase in the number of function calls.

### Factors Affecting Runtime Complexity:
- **Pivot Selection**: The choice of pivot affects the runtime complexity. Choosing a random or median-based pivot can lead to better average-case performance.
- **Partitioning Scheme**: The partitioning scheme used also impacts the runtime complexity. For example, using a "left-to-right" partitioning scheme (like in the original Quicksort algorithm) can lead to worse worst-case performance than using a "right-to-left" or "median-of-three" partitioning scheme.
- **Array Structure**: The structure of the input array can also affect the runtime complexity. For example, if the array is highly unbalanced (i.e., one side is much larger than the other), Quicksort's performance may degrade.

In general, while Quicksort has a good average-case time complexity, its worst-case time complexity can be quite poor.
