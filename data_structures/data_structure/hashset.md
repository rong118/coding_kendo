# HashSet

The HashSet implements the Set interface using a hash table so that add, remove, and contains each execute in constant or O(1) time assuming reasonable distribution of elements by their hashCode values.

<img src="../assets/hashset.png" width="350"/>

## Implementation
```c++
// c++ Implementation
std::unordered_set<std::string> q;

q.insert(5);
q.erase(5);
```

## 定义
它不允许出现重复元素, 不保证和集合中元素的顺序, 允许包含值为null的元素，但最多只能有一个null元素

它是基于HashMap实现的，HashSet底层 使用HashMap来保存所有元素，因此 HashSet 的实现比较简单，相关HashSet 的操作，基本上都是直接调用底层 HashMap的相关方法来完成



## 时间复杂度 O(1)
