# HashSet

A HashSet is a fundamental data structure that represents an unordered collection of unique elements, typically stored in a hash table. It allows for efficient insertion, deletion, and lookup operations.

## Characteristics
- Each element is associated with a unique key or identifier.
- The set does not allow duplicate elements; if you try to add a duplicate, it will be ignored.
- Lookup, insertion, and deletion operations are typically O(1) in the average case.

## Implementation
### C++ (using std::unordered_set):
```c++
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> mySet;

    // Insert some elements
    mySet.insert(1);
    mySet.insert(2);
    mySet.insert(3);

    // Check if an element is in the set
    if (mySet.find(2) != mySet.end()) {
        std::cout << "2 is in the set!" << std::endl;
    }

    // Remove an element from the set
    mySet.erase(1);

    return 0;
}
```
### Golang
```golang
package main

import (
    "fmt"
)

func main() {
    mySet := make(map[int]bool)
    // Insert some elements
    mySet[1] = true
    mySet[2] = true
    mySet[3] = true

    // Check if an element is in the set
    if _, ok := mySet[2]; !ok {
        fmt.Println("2 is not in the set!")
    }

    // Remove an element from the set
    delete(mySet, 1)
}
```

```javascript using a Set object
let mySet = new Set([1, 2, 3]);

// Check if an element is in the set
if (mySet.has(2)) {
    console.log("2 is in the set!");
}

// Remove an element from the set
mySet.delete(1);
```