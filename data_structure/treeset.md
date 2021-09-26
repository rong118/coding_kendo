# TreeSet
## 定义
几乎和hashSet一样，唯一区别是element现在有顺序
TreeSet are stored in a sorted and ascending order. TreeSet does not preserve the insertion order of elements but elements are sorted by keys.

```c++
// c++ Implementation
#include <set>;

std::set<int> s;
s.insert(11);
s.insert(22);
s.insert(33);

auto itlow=myset.lower_bound (11);    // point to 11 
auto itupper=myset.lower_bound (22);  // point to 22
```