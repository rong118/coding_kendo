# Tree Map

TreeMap: A TreeMap is a fundamental data structure that represents a sorted map, where the keys are stored in a tree-like structure. It allows for efficient insertion, deletion, and lookup operations.
In a TreeMap:

## Characteristics
- Each key-value pair is associated with a unique key or identifier.
- The set of keys is maintained in a sorted order (typically by key).

## Runtime Complexity
Lookup, insertion, and deletion operations are typically O(log n) in the average case.

## Implementation
### C++ using std::map
```c
// c++ Implementation
#include <iostream>;
#include <map>;


int main(){
  std::map<int,int> m;
  m[1] = 10;
  m[2] = 20;
  m[3] = 30;
  auto itlow = m.lower_bound(1);    //point to key 1
  auto itupper = m.upper_bound(2);  //point to key 3
  auto ret = m.equal_range(2);  // ?

  return 0;
}
```
### Golang using map and sort
```go
package main

import (
    "fmt"
)

func main() {
    m := make(map[int]int)
    m[1] = 10
    m[2] = 20
    m[3] = 30

    // Find an element in the map
    for k, v := range m {
        if k == 2 {
            fmt.Println("2 is in the map with value", v)
            break
        }
    }

    // Remove an element from the map
    delete(m, 1)

}
```
