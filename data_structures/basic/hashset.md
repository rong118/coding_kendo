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

```python
# Creating a hashset (set)
hashset = set()

# Adding elements to the hashset
hashset.add(10)
hashset.add(20)
hashset.add(30)
hashset.add(40)

# Adding duplicate elements (sets do not allow duplicates)
hashset.add(20)  # This will not be added since 20 is already in the set

# Checking if an element is in the hashset
print("Is 20 in the hashset?", 20 in hashset)  # Output: True
print("Is 50 in the hashset?", 50 in hashset)  # Output: False

# Removing an element
hashset.remove(30)  # Removes 30 from the set
print("Hashset after removing 30:", hashset)  # Output: {40, 10, 20}

# Using discard to remove an element (doesn't raise an error if element is not found)
hashset.discard(50)  # No error, even though 50 is not in the set
print("Hashset after discarding 50:", hashset)  # Output: {40, 10, 20}

# Iterating through the hashset
print("\nIterating through the hashset:")
for element in hashset:
    print(element)

# Getting the size of the hashset
print("\nSize of the hashset:", len(hashset))  # Output: 3

# Clearing the hashset
hashset.clear()
print("Hashset after clearing:", hashset)  # Output: set()
```