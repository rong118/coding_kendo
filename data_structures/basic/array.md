# Array

Array is a fundamental data structure that stores elements of the same data type in contiguous memory locations, allowing efficient random access to its elements by index.

## Implementation
### C++ Implementation
```c++
#include <iostream>
using namespace std;

int main() {
    // Declaring and initializing an array of integers in C++
    int arr[5] = {1, 2, 3, 4, 5};

    // Accessing and printing array elements
    cout << "Array elements in C++: ";
    for (int i = 0; i < 5; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### Golang Implementation
```golang
package main

import "fmt"

func main() {
    // Declaring and initializing an array of integers in Go
    arr := [5]int{1, 2, 3, 4, 5}

    // Accessing and printing array elements
    fmt.Print("Array elements in Go: ")
    for _, v := range arr {
        fmt.Printf("%d ", v)
    }
    fmt.Println()
}
```

### Python Example
```python
# Creating an Array (List)
numbers = [10, 20, 30, 40, 50]

# Accessing Elements
print(numbers[0])  # Output: 10
print(numbers[-1]) # Output: 50

# Modifying Elements
numbers[2] = 35
print(numbers)  # Output: [10, 20, 35, 40, 50]

# Using a For Loop
for num in numbers:
    print(num)

numbers = [3, 6, 1, 8, 2]

# Sorting
numbers.sort()
print(numbers)  # Output: [1, 2, 3, 6, 8]

# Reversing
numbers.reverse()
print(numbers)  # Output: [8, 6, 3, 2, 1]

# Finding Maximum and Minimum
print(max(numbers))  # Output: 8
print(min(numbers))  # Output: 1

# Summing Elements
print(sum(numbers))  # Output: 20
```

## Runtime Complexity
- **Access Time**: Accessing an element by index in an array typically has constant time complexity, O(1), because it involves simple arithmetic to calculate the memory address of the desired element based on its index.

- **Insertion/Deletion Time**: Insertion and deletion operations in arrays can have a higher time complexity, O(n), especially if they require shifting elements to maintain the array's contiguous structure. However, if the insertion/deletion happens at the end of the array, it can be done in constant time.

## Dynamic Array

A dynamic array, also known as a resizable array or a growable array, is a data structure that allows for **dynamic resizing** while maintaining the characteristics of an array, such as random access to elements and contiguous memory allocation.

Unlike static arrays, which have a fixed size determined at compile time, dynamic arrays can dynamically adjust their size during runtime to accommodate the number of elements being stored.

The key feature of dynamic arrays is their ability to automatically resize themselves when the number of elements exceeds the current capacity. When a dynamic array is full and a new element needs to be added, it typically allocates a larger chunk of memory, copies the existing elements to the new memory location, and then adds the new element.

## Implementation
### C++ Example using std::vector:
```c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // Creating a dynamic array using std::vector in C++
    vector<int> dynamicArray;

    // Adding elements to the dynamic array
    dynamicArray.push_back(1);
    dynamicArray.push_back(2);
    dynamicArray.push_back(3);

    // Accessing and printing elements of the dynamic array
    cout << "Dynamic array elements in C++: ";
    for (int i = 0; i < dynamicArray.size(); ++i) {
        cout << dynamicArray[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### Go Example using Slices:
```golang
package main

import "fmt"

func main() {
    // Creating a dynamic array using slices in Go
    dynamicArray := []int{}

    // Adding elements to the dynamic array
    dynamicArray = append(dynamicArray, 1)
    dynamicArray = append(dynamicArray, 2)
    dynamicArray = append(dynamicArray, 3)

    // Accessing and printing elements of the dynamic array
    fmt.Print("Dynamic array elements in Go: ")
    for _, v := range dynamicArray {
        fmt.Printf("%d ", v)
    }
    fmt.Println()
}
```

### Python Example using List:
```python
# Creating a dynamic array using Python's list
dynamic_array = []

# Adding elements to the dynamic array
dynamic_array.append(1)
dynamic_array.append(2)
dynamic_array.append(3)

# Removing Elements
dynamic_array.remove(2)
print(dynamic_array)

# Checking Length
print(len(dynamic_array))  # Output: 2

# Accessing and printing elements of the dynamic array
print("Dynamic array elements in Python:", " ".join(map(str, dynamic_array)))
```

## Leetcode questions
- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [4. Median of Two Sorted Arrays](../../leetcode_questions/4_median_of_two_sorted_arrays.md)
- [11. Container With Most Water](../../leetcode_questions/11_container_with_most_water.md)
- [15. 3Sum](../../leetcode_questions/15_three_sum.md)
- [26. Remove Duplicates From Sorted Array](../../leetcode_questions/26_remove_duplicates_from_sorted_array.md)
- [27. Remove Element](../../leetcode_questions/27_remove_element.md)
- [39. Combination Sum](../../leetcode_questions/39_combination_sum.md)
- [56. Merge Intervals](../../leetcode_questions/56_merge_intervals.md)
- [57. Insert Interval](../../leetcode_questions/57_insert_interval.md)
- [75. Sort Colors](../../leetcode_questions/75_sort_colors.md)
- [121. Best Time to Buy and Sell Stock](../../leetcode_questions/121_best_time_to_buy_and_sell_stock.md)
- [169. Majority Element](../../leetcode_questions/169_majority_element.md)
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
- [238. Product of Array Except Self](../../leetcode_questions/238_product_of_array_except_self.md)