# Divide And Conque

The Divide and Conquer algorithm is a problem-solving approach that breaks a problem down into smaller subproblems, solves each subproblem independently, and then combines the solutions to solve the original problem. 

This method is particularly useful for tasks that can be naturally divided into smaller, similar tasks, and it often leads to efficient and elegant solutions.

## Steps in Divide and Conquer

1. Divide: Break the problem into smaller subproblems.
2. Conquer: Solve the subproblems recursively. If the subproblem is small enough, solve it directly.
3. Combine: Combine the solutions of the subproblems to form the solution of the original problem.

## Examples

### 1. MergeSort

Merge Sort is a classic example of a Divide and Conquer algorithm:

```c++
#include <iostream>
#include <vector>

// Function to merge two subarrays
void merge(std::vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    std::vector<int> leftArr(n1);
    std::vector<int> rightArr(n2);

    // Copy data to temporary arrays
    for (int i = 0; i < n1; i++)
        leftArr[i] = arr[left + i];
    for (int i = 0; i < n2; i++)
        rightArr[i] = arr[mid + 1 + i];

    // Merge the temporary arrays back into arr[left..right]
    int i = 0; // Initial index of first subarray
    int j = 0; // Initial index of second subarray
    int k = left; // Initial index of merged subarray

    while (i < n1 && j < n2) {
        if (leftArr[i] <= rightArr[j]) {
            arr[k] = leftArr[i];
            i++;
        } else {
            arr[k] = rightArr[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of leftArr, if any
    while (i < n1) {
        arr[k] = leftArr[i];
        i++;
        k++;
    }

    // Copy the remaining elements of rightArr, if any
    while (j < n2) {
        arr[k] = rightArr[j];
        j++;
        k++;
    }
}

// Function to implement Merge Sort
void mergeSort(std::vector<int>& arr, int left, int right) {
    if (left < right) {
        // Find the middle point
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arr_size = arr.size();

    std::cout << "Given array is \n";
    for (int i = 0; i < arr_size; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;

    mergeSort(arr, 0, arr_size - 1);

    std::cout << "\nSorted array is \n";
    for (int i = 0; i < arr_size; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
    return 0;
}
```

### 2. Finding the maximum and minimum elements in an array:

```c++
#include <iostream>
#include <vector>
#include <limits.h>

using namespace std;

// Struct to hold the results
struct MinMax {
    int min;
    int max;
};

// Function to find the minimum and maximum using Divide and Conquer
MinMax findMinMax(const vector<int>& arr, int left, int right) {
    MinMax result, leftResult, rightResult;

    // If the array has only one element
    if (left == right) {
        result.min = arr[left];
        result.max = arr[left];
        return result;
    }

    // If the array has two elements
    if (right == left + 1) {
        if (arr[left] < arr[right]) {
            result.min = arr[left];
            result.max = arr[right];
        } else {
            result.min = arr[right];
            result.max = arr[left];
        }
        return result;
    }

    // Divide the array into two halves
    int mid = left + (right - left) / 2;
    leftResult = findMinMax(arr, left, mid);
    rightResult = findMinMax(arr, mid + 1, right);

    // Combine the results
    result.min = min(leftResult.min, rightResult.min);
    result.max = max(leftResult.max, rightResult.max);

    return result;
}

int main() {
    vector<int> arr = {100, 11, 445, 1, 330, 3000};
    int n = arr.size();

    MinMax result = findMinMax(arr, 0, n - 1);

    cout << "Minimum element is " << result.min << endl;
    cout << "Maximum element is " << result.max << endl;

    return 0;
}
```

## Runtime Complexity

The runtime complexity of a Divide and Conquer algorithm can vary depending on how the problem is divided and how the solutions are combined.

Generally, it can be relations of the form:

T(n) = a * T(b/n) + f(n)

- T(n) is the time complexity of the algorithm.
- a is the number of subproblems into which the problem is divided.
- n/b is the size of each subproblem.
- f(n) is the cost of dividing the problem and combining the results of the subproblems.

For example, The recurrence relation for Merge Sort is: 

T(n) = 2 * T(2 * n) + O(n)

After applying the Master Theorem, T(n) = O(nlogn)