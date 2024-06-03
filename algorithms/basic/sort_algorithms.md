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

Merge sort is a sorting algorithm that combines two sorted arrays into a single, sorted array. It's a **stable** sorting algorithm, which means it maintains the relative order of equal elements.

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

## IV. Quick Sort

Quick sort is a high efficient sorting algorithm developed by Tony Hoare in 1962. It is an in-place sorting algorithm, which means it doesn't require any extra space to store the elements being sorted.

The key idea behind Quicksort is that it uses the pivot element as a "divider" to split the array into two smaller arrays: one with elements less than the pivot and another with elements greater than the pivot. This partitioning step makes it possible to sort the entire array using only a few recursive calls.

### C++ Implementation
```c++
#include <iostream>
using namespace std;

// Function to swap two elements
void swap(int* a, int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}

// Function to partition the array and return the pivot index
int partition(int arr[], int low, int high) {
    int pivot = arr[high]; // Choose the last element as the pivot
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++; // Increment index of smaller element
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[i + 1], &arr[high]); // Move pivot to its correct position

    return (i + 1);
}

// Function to implement QuickSort
void quicksort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // Partition the array and get the pivot index

        // Recursively sort subarrays on either side of the pivot
        quicksort(arr, low, pi - 1);
        quicksort(arr, pi + 1, high);
    }
}

// Function to print an integer array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};

    int n = sizeof(arr) / sizeof(arr[0]);

    // Display the original array
    cout << "Original array: ";
    printArray(arr, n);

    // Sort the array using Quicksort
    quicksort(arr, 0, n - 1);

    // Display the sorted array
    cout << "Sorted array: ";
    printArray(arr, n);

    return 0;
}
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
