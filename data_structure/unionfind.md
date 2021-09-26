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
    DSU(int N){  //O(N)
        parent.resize(N);

        for(int i = 0; i < parent.size(); i++){
            parent[i] = i;
        }
    }

    //
    int _find(int x){
        if(parent[x] != x) parent[x] = _find(parent[x]);
        return parent[x];
    }
    
    //
    void _union(int a, int b){
        parent[_find(x)] = _find(y);
        return;
    }
}
```

## 优化
- path compression 
- union by rank