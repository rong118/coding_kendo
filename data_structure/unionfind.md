# Union Find
## 定义
并查集 是一种树形的数据结构，用于处理不交集的合并 (union)及 查询(find)问题。找几个数字是否在同一个 group里面
- Find:确定元素属于哪一个子集。它可以被用来确定两个元素是否 属于同一子集。
- Union:将两个子集合并成同一个集合。

<img src="../assets/unionfind.png" width="400" />

union(x, y) find(x)时间复杂度极快,接近常数级别 log* is the iterated logarithm.

## Basic implementation
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

## 优化
- improve with size (weighted)

<img src="../assets/weighted_quick_union.png" width="400" />

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
- union by rank

<img src="../assets/union_by_rank.png" width="500" />

```c++
class DSU {
public:
    vector<int> parent;
    vector<int> rank;
    DSU(int N){
        parent.resize(N);
        rank.resize(N, 1);

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
        if(rootx == rooty) return;
        if(rank[rootx] < rank[rooty]){
            parent[rootx] = rooty;
        }else if(rank[rootx] > rank[rooty]){
            parent[rooty] = rootx;
        }else{
            parent[rootx] = rooty;
            rank[rooty]++;
        }
        return;
    }
}
```

## 复杂度
- 使用 quick union 版本的 并查集， 性能和深度有关系O(h).
但是并查集并不是一个2叉树， 所以时间复杂度是O(log*n)
- iterated logarithm O(log*n) 接近 O(1), 比O(1) 慢一点

## Leetcode questions
- [305 Number of Island II](../leetcode_questions/305_number_of_island_ii.md)
- [547 Friend Circles](../leetcode_questions/547_friend_circles.md)
- [128 Longest Consecutive Sequence](../leetcode_questions/128_longest_consecutive_sequence.md)
- [261 Graph Valid Tree](../leetcode_questions/261_graph_valid_tree.md)