# Hash Map

In computing, hash map is a data structure that implements an associative array or dictionary. It is an abstract data type that maps keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found.

A hash map typically uses a single array or linked list to store values.

## Implementation
### C++ using std::unordered_map
```c++
#include <iostream>
#include <string>
#include <unordered_map>

int main() {
    std::unordered_map<std::string, int> myMap;

    // Insert some key-value pairs
    myMap["foo"] = 1;
    myMap["bar"] = 2;
    myMap["baz"] = 3;

    // Look up a value
    if (myMap.find("foo") != myMap.end()) {
        std::cout << "Value for 'foo' is: " << myMap["foo"] << std::endl;
    }

    return 0;
}
```
### Golang using map
```go
package main

import (
    "fmt"
)

func main() {
    m := map[string]int{"foo": 1, "bar": 2, "baz": 3}

    // Look up a value
    if val, ok := m["foo"]; ok {
        fmt.Println("Value for 'foo' is:", val)
    }
}
```

### Javascript using object
```javascript
const myMap = {
  foo: 1,
  bar: 2,
  baz: 3,
};

// Look up a value
console.log(`Value for 'foo' is ${myMap.foo}`);
```

## O(1) search and insert 
- Insertion (put(key, value)): O(1) <br>
In a well-implemented HashMap, insertion is typically done in constant time, as it only requires calculating the hash code for the key and updating the bucket array.
- Lookup (get(key)): O(1) <br>
Looking up a value by its key is also typically done in constant time, as it only requires hashing the key and finding the corresponding bucket.
- Deletion (remove(key)): O(1) <br>
Deleting an entry from the HashMap is often done in constant time, as it simply involves updating the bucket array and removing any necessary links.
- Contains Key (containsKey(key)): O(1) <br>
Checking if a key exists in the HashMap is typically done in constant time, as it only requires hashing the key and finding the corresponding bucket.