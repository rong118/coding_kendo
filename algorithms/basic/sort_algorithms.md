# Sorting Algortihms

Sorting algorithms are procedures that take an unsorted collection (or array) as input and produce a sorted collection as output. The goal is to arrange the elements in a specific order.

## Types of Sorting Algorithms

There are many sorting algorithms, each with its strengths and weaknesses. Some common types include:

- **Comparison-Based Sorting**: These algorithms compare elements to determine their order. Examples: **Bubble Sort**, **Selection Sort**, **Insertion Sort**, **Merge Sort**
- **Non-Comparison-Based Sorting**: These algorithms don't rely on comparisons. Examples: **QuickSort**, **Radix Sort**, **Counting Sort**
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

## III. Merge Sort

Merge sort is a popular sorting algorithm that combines two sorted arrays into a single, sorted array. It's a **stable** sorting algorithm, which means it maintains the relative order of equal elements.

### C++ Implementation
```c++
#include   <iostream>
#include   <vector>

void merge(int arr[], int left, int mid, int right) {
    // Create temporary arrays for the two halves
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2]; // Temporary arrays

    // Copy elements from original array to temporary arrays
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Initialize indices for the two halves
    int i, j, k;
    i = 0;
    j = 0;
    k = left;

    // Merge two halves into one array
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    // Copy remaining elements from left half, if any
    while (i < n1) {
        arr[k++] = L[i++];
    }

    // Copy remaining elements from right half, if any
    while (j < n2) {
        arr[k++] = R[j++];
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        // Find the middle point of the array
        int mid = (left + right) / 2;

        // Recursively sort the two halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
}

// Main function to test the Merge Sort algorithm
int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};

    int n = sizeof(arr) / sizeof(arr[0]);

    // Display the original array
    std::cout << "Original array: ";
    printArray(arr, n);
    mergeSort(arr, 0, n - 1);

    // Display the sorted array
    std::cout << "Sorted array: ";
    printArray(arr, n);

    return 0;
}
```

### Runtime Complexity

Merge sort has a time complexity of **O(nlogn)**, where n is the length of the input array. The space complexity is O(n), as we need to store the temporary arrays during the merging process.
