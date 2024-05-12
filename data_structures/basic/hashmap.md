# HashMap

In computing, hash map is a data structure that implements an associative array or dictionary. It is an abstract data type that maps keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found.

slot_index = hash(key)

During lookup, the key is hashed and the resulting hash indicates where the corresponding value is stored.

<img src="../assets/hashmap.png" width="400"/>

## Implementation
```c
// c++ Implementation
#include <iostream>
#include <map>

using namespace std;

int main() {
  std::unordered_map<int, int> m;
  
  m[44] = 11;
  m[11] = 33;

  int r = m.at(11);  // 33
  m.erase(44);
  m.insert({22, 66});

  return 0;
}
```

```go

```

## O(1) search and insert 

## Collision resolution

* Separate chaining
* Open addressing



如果2个不同的string input作为key在hashmap中index 出现了冲突如何处理?
一般使用两种方法
1. 挂链表 Separate Chaining
2. 开放地址法 open addressing

好处:查找比纯链表快，插入删除比纯数组快
