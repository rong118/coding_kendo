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

```go
// Go Implementation
package main

import "fmt"

func main() {
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1])

	primes := [6]int{2, 3, 5, 7, 11, 13}
	fmt.Println(primes)
}
```

## Features
- Most common data structure
- Access data by index O(1)
- Array size cannot be changed
- Add/Delete operatings are slow due to re-malloc memory