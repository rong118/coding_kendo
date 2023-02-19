# Array

In computer science, an array is a data structure **consisting of a collection of elements** (values or variables), each identified by at least one array index or key.

## Implementation
```c++
// C++ Implementation
#include <iostream>
using namespace std;

int main() {
  int numbers[5] = {7, 5, 6, 12, 35};

  cout << "The numbers are: ";
  //  Printing array elements
  // using range based for loop
  for (const int &n : numbers) {
    cout << n << "  ";
  }

  cout << "\nThe numbers are: ";
  //  Printing array elements
  // using traditional for loop
  for (int i = 0; i < 5; ++i) {
    cout << numbers[i] << "  ";
  }

  return 0;
}
```

## Features
- Access data by index O(1)
- Array size cannot be changed
- Add/Delete operatings are slow due to re-malloc memory

## Dynamic Array

A dynamic array is an array with a big improvement: **automatic resizing**. One limitation of arrays is that they're fixed size, meaning you need to specify the number of elements your array will hold ahead of time. A dynamic array expands as you add more elements. So you don't need to determine the size ahead of time.

## Implementation
```c++
// C++ Implementation
#include <iostream>
#include <vector>
using namespace std;

int main() {
  // STL vector<T>
  vector<int> numbers = {7, 5, 6, 12, 35};

  cout << "The numbers are: ";
  //  Printing array elements
  // using range based for loop
  for (const int &n : numbers) {
    cout << n << "  ";
  }

  numbers.push_back(46); // {7, 5, 6, 12, 35, 46}

  cout << "\nThe numbers are: ";
  //  Printing array elements
  // using traditional for loop
  for (int i = 0; i < numbers.size(); ++i) {
    cout << numbers[i] << "  ";
  }

  return 0;
}
```

## Leetcode questions
- [1. Two Sum](../leetcode_questions/1_two_sum.md)
- [4. Median of Two Sorted Arrays](../leetcode_questions/4_median_of_two_sorted_arrays.md)
- [11. Container With Most Water]()
- [15. 3Sum](../leetcode_questions/15_three_sum.md)
- [26. Remove Duplicates From Sorted Array](../leetcode_questions/26_remove_duplicates_from_sorted_array.md)
- [27. Remove Element](../leetcode_questions/27_remove_element.md)
- [39. Combination Sum]()
- [56. Merge Intervals](../leetcode_questions/56_merge_intervals.md)
- [57. Insert Interval](../leetcode_questions/57_insert_interval.md)
- [75. Sort Colors](../leetcode_questions/75_sort_colors.md)
- [121. Best Time to Buy and Sell Stock](../leetcode_questions/121_best_time_to_buy_and_sell_stock.md)
- [169. Majority Element](../leetcode_questions/169_majority_element.md)
- [217. Contains Duplicate](../leetcode_questions/217_contain_duplicate.md)
- [238. Product of Array Except Self](../leetcode_questions/238_product_of_array_except_self.md)