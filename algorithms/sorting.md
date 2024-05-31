# Sorting Algortihms

Sorting algorithms are procedures that take an unsorted collection (or array) as input and produce a sorted collection as output. The goal is to arrange the elements in a specific order.

## Types of Sorting Algorithms

There are many sorting algorithms, each with its strengths and weaknesses. Some common types include:

- **Comparison-Based Sorting**: These algorithms compare elements to determine their order. Examples: Bubble Sort, Selection Sort, Insertion Sort, Merge Sort
- **Non-Comparison-Based Sorting**: These algorithms don't rely on comparisons. Examples: QuickSort, Radix Sort, Counting Sort
- **Hybrid Sorting**: Combines multiple sorting techniques. Examples: Timsort (used in Java), Introsort (used in C++)

## I. Bubble Sort

Bubble Sort is a simple, comparison-based sorting algorithm that repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

### C++ Implementation
```c++
#include <iostream>
#include <vector>

void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) {
            break; // early exit if the list is already sorted
        }
    }
}

int main() {
    std::vector<int> arr = {4, 2, 7, 1, 3};
    bubbleSort(arr);
    for (int x : arr) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

### Runtime Complexity of Bubble Sort:
The runtime complexity of Bubble Sort is **O(n^2)**, where n is the number of elements in the input array.

## II. Selection Sort

Selection sort is a simple, comparison-based sorting algorithm that repeatedly finds the minimum element from unsorted part and puts it at the beginning. The input list is divided into two parts: sorted part and unsorted part.

### C++ Implementation
```c++
#include  <iostream>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        // Find the minimum element in unsorted part
        int minIndex = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        // Swap found minimum with first element of unsorted part
        swap(arr[i], arr[minIndex]);
    }
}

int main() {
    int arr[] = {5, 2, 8, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    selectionSort(arr, n);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### Runtime Complexity of Selection Sort
Selection Sort has a runtime complexity of O(n^2), where n is the number of elements in the input array.
