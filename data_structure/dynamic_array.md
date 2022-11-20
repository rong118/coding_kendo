# Dynamic Array

A dynamic array is an array with a big improvement: **automatic resizing**. One limitation of arrays is that they're fixed size, meaning you need to specify the number of elements your array will hold ahead of time. A dynamic array expands as you add more elements. So you don't need to determine the size ahead of time.

## Implementation
```c++
// C++ Implementation
#include <iostream>
#include <vector>
using namespace std;

int main() {
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

```go
package main

import (
	"github.com/emirpasic/gods/lists/arraylist"
	"github.com/emirpasic/gods/utils"
)

func main() {
    // Slice is a dynamically-sized in Go
    var s []int
	s = append(s, 0) // append works on nil slices.
	printSlice(s)
	s = append(s, 1) // The slice grows as needed.
	printSlice(s)
	s = append(s, 2, 3, 4) // We can add more than one element at a time.
	printSlice(s)

    // Or use arraylist from gods
	list := arraylist.New()
	list.Add("a")                         // ["a"]
	list.Add("c", "b")                    // ["a","c","b"]
	_, _ = list.Get(0)                    // "a",true
	_, _ = list.Get(100)                  // nil,false
	_ = list.Contains("a", "b", "c")      // true
	_ = list.Contains("a", "b", "c", "d") // false
	list.Swap(0, 1)                       // ["b","a",c"]
	list.Remove(2)                        // ["b","a"]
	list.Remove(1)                        // ["b"]
	list.Remove(0)                        // []
	_ = list.Empty()                      // true
	_ = list.Size()                       // 0
	list.Add("a")                         // ["a"]
	list.Clear()                          // []
	list.Insert(0, "b")                   // ["b"]
	list.Insert(0, "a")                   // ["a","b"]
}
```