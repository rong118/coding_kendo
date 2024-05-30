# Union-Find (Disjoint-Set)

The Union-Find, also known as the Disjoint-Set, is a tree-like data structure used for handling the union and find operations on disjoint sets. 

It determines whether several elements are in the same group.

## Key characteristics

A Union-Find data structure represents a set of elements, where each element belongs to one or more groups (sets). The primary operations are:

- **MakeSet**: Create a new set containing a given element.
- **Find**: Determines which subset a particular element is in. This can be used to determine if two elements are in the same subset.
- **Union**: Joins two subsets into a single subset.

## Implmentation
### C++
```c++
class DSU {
public:
    vector<int> parent;
    DSU(int N){
        parent.resize(N);

        for(int i = 0; i < parent.size(); i++){
            parent[i] = i;
        }
    }

    int _find(int x){
        if(parent[x] != x) parent[x] = _find(parent[x]);
        return parent[x];
    }
    
    void _union(int x, int y){
        parent[_find(x)] = _find(y);
        return;
    }
}
```

### Golang
```golang
package main

import (
    "fmt"
)

type UnionFind struct {
    parent []int
    n      int
}

func NewUnionFind(n int) *UnionFind {
    return &UnionFind{n, make([]int, n)}
}

func (uf *UnionFind) Find(x int) int {
    if uf.parent[x] != x {
        uf.parent[x] = uf.Find(uf.parent[x])
    }
    return uf.parent[x]
}

func (uf *UnionFind) UnionSet(x, y int) {
    rootX := uf.Find(x)
    rootY := uf.Find(y)

    if rootX != rootY {
        uf.parent[rootX] = rootY
    }
}

func main() {
    uf := NewUnionFind(5) // Create a Union-Find data structure for 5 elements

    uf.UnionSet(1, 2)
    uf.UnionSet(2, 3)
    uf.UnionSet(4, 5)

    fmt.Println("Root of set containing 1:", uf.Find(1))
    fmt.Println("Root of set containing 2:", uf.Find(2))
    fmt.Println("Root of set containing 3:", uf.Find(3))
    fmt.Println("Root of set containing 4:", uf.Find(4))
    fmt.Println("Root of set containing 5:", uf.Find(5))

}
```

## Optimize Implementation

The most efficient implementation uses two techniques: 
- **Path Compression**
- **Union by Rank/Size**

### Union by Size Example
```c++
class DSU {
public:
    vector<int> parent;
    vector<int> size;
    DSU(int N){
        parent.resize(N);
        size.resize(N, 1);

        for(int i = 0; i < parent.size(); i++){
            parent[i] = i;
        }
    }

    int _find(int x){
        if(parent[x] != x) parent[x] = _find(parent[x]);
        return parent[x];
    }
    
    void _union(int x, int y){
        int rootx = _find(x);
        int rooty = _find(y);
        if(size[rootx] <= size[rooty]){
            parent[rootx] = rooty;
            size[rooty] += rootx;
        }else{
            parent[rooty] = rootx;
            size[rootx] += rooty;
        }
        return;
    }
}
```

## Runtime Complexity

The runtime complexity of these operations depends on the implementation of the data structure. The most efficient implementation uses two techniques: **path compression** and **union by rank/size**.

### Techniques

- Path Compression:
  This technique flattens the structure of the tree whenever find is called, by making each node point directly to the root. This drastically reduces the time complexity of future operations.
- Union by Rank/Size:
  This technique ensures that the smaller tree (rank/size) is always added under the root of the larger tree (rank/size). This keeps the tree as flat as possible.

### Complexity

When both path compression and union by rank/size are used, the amortized time complexity for both the find and union operations is nearly constant. Specifically, the time complexity is:

- Find operation: **O(α(n))**
- Union operation: **O(α(n))**

α(n) is the inverse Ackermann function, which grows extremely slowly. For all practical purposes, α(n) can be considered a constant.

## Leetcode Questions
- [305 Number of Island II](../leetcode_questions/305_number_of_island_ii.md)
- [547 Friend Circles](../leetcode_questions/547_friend_circles.md)
- [128 Longest Consecutive Sequence](../leetcode_questions/128_longest_consecutive_sequence.md)
- [261 Graph Valid Tree](../leetcode_questions/261_graph_valid_tree.md)
