# Binary Index Tree

A Binary Indexed Tree (BIT) is a data structure used to efficiently calculate prefix sums and cumulative values of an array or vector.

## How BIT works:

- **Initialization**: Create an array BIT with the same length as the original array, initialized to zero.

- **Insert**: When updating an element at index i, calculate the prefix sum from 0 to i-1 and store it in BIT[i].

- **Query**: To compute the cumulative sum from start to end, traverse the BIT from BIT[start-1] to BIT[end]. The key insight is that you can skip certain nodes by using binary indexing (bit manipulation) to determine whether a node should be included in the sum or not.

## Implementation
### C++ Implementation
```c++
#include <iostream>
#include <vector>

class BIT {
public:
    std::vector<int> bit;

    BIT(int n) : bit(n + 1, 0) {}

    void update(int i, int val) {
        for (; i < (int)bit.size(); i += (i & -i)) {
            bit[i] += val;
        }
    }

    int query(int i) {
        int sum = 0;
        for (; i > 0; i -= (i & -i)) {
            sum += bit[i];
        }
        return sum;
    }
};

int main() {
    BIT bit(10); // Initialize a BIT of size 10

    std::vector<int> arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; // Example array

    for (int i = 0; i < arr.size(); i++) {
        bit.update(i, arr[i]); // Update the BIT with the values from the array
    }

    std::cout << "Cumulative sum from index 2 to 5: " << bit.query(4) << std::endl; // Calculate the cumulative sum for the range [2, 5]

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
    "fmt"
)

type BIT struct {
    bit []int
}

func NewBIT(n int) *BIT {
    return &BIT{make([]int, n+1, 0)}
}

func (bit *BIT) Update(i int, val int) {
    for ; i < len(bit.bit); i += i & -i {
        bit.bit[i] += val
    }
}

func (bit *BIT) Query(i int) int {
    sum := 0
    for ; i > 0; i -= i & -i {
        sum += bit.bit[i]
    }
    return sum
}

func main() {
    bit := NewBIT(10)
    arr := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10} // Example array

    for i, v := range arr {
        bit.Update(i, v) // Update the BIT with the values from the array
    }

    fmt.Println("Cumulative sum from index 2 to 5:", bit.Query(4)) // Calculate the cumulative sum for the range [2, 5]
}
```

### Binary searching by i & -i

In the Go code, the line for ; i > 0; i -= i & -i { ... } is a loop that iterates through the bits of the index i.

- i & -i is a bitwise operation that finds the highest bit set in i. In binary, this would be equivalent to finding the most significant 1 bit.

- i -= i & -i updates the value of i by subtracting the highest bit set in i. This effectively "moves" the loop to the next least significant bit.

This technique is called "**bit twiddling**" or "**binary searching**", and it's used to efficiently iterate through the bits of an integer. By repeatedly updating i to the next lowest bit, we can traverse the binary representation of i from most significant bit to least significant bit.

In the context of the BIT implementation, this loop is used in both the Update and Query methods to efficiently calculate the cumulative sum or update the BIT values.

## Runtime Complexity

The runtime complexity of a Binary Indexed Tree (BIT) depends on the operation being performed:

### - Update

The update operation has an average-case time complexity of O(log n), where n is the size of the BIT. This is because we only need to traverse the BIT up to the highest bit set in the updated index.

### - Query

The query operation has an average-case time complexity of O(log n) as well, since we need to traverse the BIT from the highest bit set in the start index down to the lowest bit set in the end index.

## LeetCode Questions
- [307. Range Sum Query - Mutable]()
- [308. Range Sum Query 2D]()
- [315. Count of Smaller Numbers After Self]()
- [327. Count of Range Sum]()
- [440. K-th Smallest in Lexicographical Order]()
